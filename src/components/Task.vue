<template>
  <div class="task" :class="{'task-complete' : taskDone}">
    <p>
      <span class="task-index">{{taskIndex}}</span>
      <span class="task-name">{{taskName}}</span>
      <!-- <input class="task-complete-box" type="checkbox" v-model="taskDone" @click="updateListAtIndex"> -->
      <input class="task-complete-box" type="checkbox" v-model="taskDone" @change="updateListCompletion">
      <button class="task-delete-button" @click="deleteTask" v-if="taskDone">X</button>
    </p>
  </div>
</template>

<script lang="ts">

import { Vue, Prop, Component } from 'vue-property-decorator'

@Component
export default class Task extends Vue {
  @Prop() taskIndex!: number;
  @Prop() taskName!: string;
  @Prop() taskDone!: boolean;

  deleteTask () {
    this.$root.$emit('deleteTask', this.taskIndex)
    // console.log(this.taskIndex)
  }

  updateListCompletion () {
    // this.taskDone = !this.taskDone
    this.$root.$emit('updateListCompletion', this.taskIndex, this.taskDone)

    if (this.taskDone === true) {
      this.$root.$emit('pushTaskToTheEnd', this.taskIndex)
      // console.log(this.taskIndex)
    }
  }

  taskAsObject (): object {
    return {
      taskIndex: this.taskIndex,
      taskName: this.taskIndex,
      taskDone: this.taskIndex
    }
  }
}

</script>

<style lang="scss">

.task {
  text-align: left;
  transition-duration: 0.2s;
  margin-left: 3rem;
  suffix: "\20\20";
}

.task:hover {
  // text-decoration: underline;
  // background-color: #555;
  color: #4DB6AC
}

.task-complete {
  text-decoration: line-through;
}

.task-name {
  margin: 0.7rem 2rem;
}

.task-complete-box {
  text-align: left;
}

.task-complete-box {
  margin-right: 1rem;
}

</style>
