<template>
    <div>
        <!-- <p>{{randoproperty}}</p> -->
        <div>
            <Task v-for="task in taskList" :key="task" :taskName="task.name" :taskDone="task.done" :taskIndex="taskList.indexOf(task)"></Task>
        </div>
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
