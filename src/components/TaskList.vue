<template>
    <div>
        <!-- <p>{{randoproperty}}</p> -->
        <!-- <div> -->
          <transition-group name="flip-list" tag="div">
            <Task v-for="task in taskList" :key="task" :taskName="task.name" :taskDone="task.done" :taskIndex="taskList.indexOf(task)"></Task>
          </transition-group>
        <!-- </div> -->
    </div>
</template>

<script lang="ts">

import { Vue, Prop, Component } from 'vue-property-decorator'
import Task from './Task.vue'

@Component({
  components: {
    Task
  }
})

export default class TaskList extends Vue {
  @Prop() taskList!: Array<Task>;
  @Prop() randoproperty!: string;
}

</script>

<style lang="scss" scoped>

.flip-list-move {
  transition: transformation 1s;
}

</style>
