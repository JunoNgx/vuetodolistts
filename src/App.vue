<template>
  <div id="app">
    <Header/>
    <InputField label='Enter new task: ' @addTaskFromInput="addTask" />
    <TaskList randoproperty="This is a randomly parsed property" :taskList="todoList" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Header from './components/Header.vue'
import TaskList from './components/TaskList.vue'
import InputField from './components/InputField.vue'

@Component({
  components: {
    Header,
    TaskList,
    InputField
  }
})

export default class App extends Vue {
  todoList = [
    {
      name: 'Learn Elm',
      done: false
    },
    {
      name: 'Play pico-8',
      done: false
    },
    {
      name: 'Watch StarCraft',
      done: true
    }
  ]

  // public addTask (task: { name: string; done: boolean }) {
  public addTask (taskName: string) {
    this.todoList.unshift({ name: taskName, done: false })
  }
}

</script>

<style lang="scss">

$font-fam: "Roboto Condensed", Helvetica, sans-serif;

#app {
  font-family: $font-fam;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #555;
  max-width: 400px;
  margin: auto;
  border: 2px solid #555;
  padding: 2rem;
}

body {
  background-color: #eee;
}

button {
  // -webkit-appearance: button;
  // -webkit-writing-mode: horizontal-tb !important;
  // text-rendering: auto;
  // color: buttontext;
  // letter-spacing: normal;
  // word-spacing: normal;
  // text-transform: none;
  // text-indent: 0px;
  // text-shadow: none;
  // display: inline-block;
  // text-align: center;
  // align-items: flex-start;
  // cursor: default;
  background-color: #bbb;
  // box-sizing: border-box;
  // margin: 0em;
  font-family: $font-fam;
  padding: 2px 7px;
  // border-width: 2px;
  // border-style: outset;
  // border-color: buttonface;
  // border-image: initial;
  border: none;
}

button:focus {
    outline: #4DB6AC auto 1px;
}

</style>
