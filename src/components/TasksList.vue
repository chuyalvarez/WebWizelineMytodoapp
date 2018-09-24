<template>
  <div>
    <h3>{{ title }}</h3>


      <ul>
        <li v-for="(task, index) in taskList" :key="index">
          <div class="card blue-grey darken-1">
            <div class="card-content white-text">
              <div class="row">
                <div class="col s8">
                  {{ task.name }}
                </div>
                <div class="col s4 center">
                  <button class="btn waves-effect waves-light green" v-if="!task.done" type="button" @click="toggleTasks(task)">Completar</button>
                </div>
              </div>
            </div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    taskList: {
      type: Array,
      required: true
    }
  },
  methods: {
    toggleTasks (task) {
      this.$emit('completar', task)
    }
  }
}
</script>
