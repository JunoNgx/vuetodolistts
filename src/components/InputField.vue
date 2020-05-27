<template>
  <div>
    <label for="input-field"> {{label}}  </label>
    <input id="input-field" type="text" v-model="newTask" @keyup.enter="checkInput">
    <button @click="checkInput">Enter</button>
    <p v-show="error" class="error" >Task name cannot be blank</p>
  </div>
</template>

<script lang="ts">
import { Vue, Prop, Component } from 'vue-property-decorator'

@Component
export default class InputField extends Vue {
  @Prop({ required: true })label!: string;

  newTask = 'Practice StarCraft';
  error = false;

  addTask () {
    this.$emit('addTaskFromInput', this.newTask)
    this.newTask = ''
    // console.log('adding')
  }

  checkInput () {
    if (this.newTask === '') {
      this.error = true
    } else {
      this.addTask()
      this.error = false
      console.log('error is false')
    }
  }
}
</script>

<style lang="scss" scoped>

input {
  margin-right: 0.5rem;
}

p.error {
  font-size: 14px;
  color: #CD5C5C;
}

#input-field {
  width: 150px;
}

</style>
