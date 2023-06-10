<template>
  <header>
    <h2>Create Your Own <span class="green">Task</span></h2>
  </header>
  <main>
    <div class="list-task">
      <p>{{ tasks.length === 0 ? empty : '' }}</p>
      <div v-for="(item, index) in tasks" class="item-task" :class="{'task-done': item.isDone}" >
        <div class="task-body">
          <input
            type="checkbox"
            name="status"
            :checked="item.isDone"
            @change="taskFinished(index)"
            :disabled="item.isDone"
          />
          <div class="task-text">
            <div class="title-task">
              {{ item.title.toUpperCase() }}
            </div>
            <div class="description-task">
              {{ item.description }}
            </div>
          </div> 
        </div>
        <button type="button" class="delete" @click="removeTask(index), inputEmpty=''">Delete</button>
      </div>
    </div>
    <div class="action">
      <p class="failed-add">{{ inputEmpty }}</p>
      <a href="#" class="add-button" v-if="!isCreating" @click="inputEmpty = '', isCreating = !isCreating">{{ tasks.length === 0 ? 'Create Task ?' : 'Add Task' }}</a>
      <div class="add-card" v-else>
        <div class="card">
            <input v-model="titleValue" class="form-control" placeholder="Title" type="text">
            <textarea v-model="descriptionVal" class="form-control" placeholder="Description"
            rows="8"></textarea>
        </div>
        <div class="button-wrapper">
          <button class="btn btn-primary" @click="addTask(), clearInput(), isCreating = !isCreating">Save</button>
          <button class="btn btn-outline-secondary" @click="clearInput(), isCreating = !isCreating">Cancel</button>
        </div>
      </div>
      
    </div>
  </main>
  <footer>
    <p>Copyright © <span class="green">2023</span></p>
  </footer>
</template>

<script>

export default {
  data() {
    return {
      tasks: [],
      isCreating: false,
      titleValue: '',
      descriptionVal: '',
      empty: `There's No Task Yet`,
      isDone: false,
      inputEmpty: ''
    }
  },
  methods: {
    addTask() {
      if ( !this.titleValue || !this.descriptionVal ) {
        this.inputEmpty = 'Create Task Failed! Make Sure the Input Field not Empty'
      }
      else {
        this.tasks.unshift({
          title: this.titleValue,
          description: this.descriptionVal
        })
      }
    },
    removeTask(index) {
        this.tasks.splice(index, 1)
    },
    clearInput() {
      this.titleValue = '',
      this.descriptionVal = ''
    },
    taskFinished(index) {
      this.tasks[index].isDone = !this.tasks[index].isDone
    }
  }
}
</script>
