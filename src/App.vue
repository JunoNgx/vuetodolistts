<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <Header/>
    <TaskList randoproperty="This is a randomly parsed property" :taskList="todoList" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator'
import Header from './components/Header.vue'
import TaskList from './components/TaskList.vue'

@Component({
  components: {
    Header,
    TaskList
  }
})

export default class App extends Vue {
  todoList = [
    {
      name: 'Write app',
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
  ];
}

</script>

<style lang="scss">
#app {
  font-family: "Roboto Condensed", Helvetica, Arial, sans-serif;
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
</style>
