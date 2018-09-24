<template>
  <div>
    <h1 class="center">My ToDo App</h1>
    <div class="row">

            <form @submit.prevent="addTask">
                <div class="col s4">
                  <input class= "grey darken-1"v-model="newTaskName" type="text">
                </div>
                <div class="col s4">
                  <button class="btn waves-effect waves-light grey darken-1" type="submit">Agregar Tarea
                  </button>
                </div>
            </form>

    </div>

    <div class="row">
      <div class="col s4">
        <tasks-list :title="'Pendientes'" :task-list="tasksPending" @completar="toggleTask"/>
      </div>
    </div>
    <br>

    <hr>
    <div class="row">
      <div class="col s4">
        <tasks-list :title="'Completados'" :task-list="tasksDone" @completar="toggleTask"/>
      </div>
    </div>
  </div>
</template>

<script>
import TasksList from './components/TasksList'


export default{
  components: {
    TasksList
  },
  data () {
    return {
      newTaskName: '',
      tasks: []
    }
  },
  mounted () {
    const todos = JSON.parse(this.$localStorage.get('tasks'))
    if (todos) {
      this.tasks = todos
    }
  },
  methods: {
    toggleTask (task) {
      task.done = !task.done
      this.$localStorage.set('tasks', JSON.stringify(this.tasks))

    },
    addTask () {
    if(!this.newTaskName) return
     this.tasks.push({
      name: this.newTaskName,
      done: false
     })
     this.newTaskName = ''
     this.$localStorage.set('tasks', JSON.stringify(this.tasks))
    }
  },
  computed:{
    tasksPending (){
      return this.tasks.filter(task => !task.done)
    },
    tasksDone (){
      return this.tasks.filter(task => task.done)
    }
  }
}
</script>
