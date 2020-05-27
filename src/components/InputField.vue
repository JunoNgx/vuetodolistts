<template>
  <div>
    <label for="input-field"> {{label}}  </label>
    <input id="input-field" type="text" v-model="newTask" @keyup.enter="addTask">
    <button @click="addTask">Enter</button>
  </div>
</template>

<script lang="ts">
import { Vue, Prop, Component } from 'vue-property-decorator'

@Component
export default class InputField extends Vue {
  @Prop({ required: true })label!: string;

  newTask = 'Watch weekly StarCraft';

  addTask () {
    this.$emit('addTaskFromInput', this.newTask)
    this.newTask = ''
    // console.log('adding')
  }
}
</script>

<style lang="scss" scoped>

input {
  margin-right: 0.5rem;
}

</style>
