<template>
  <div id="app">
    <Header :owner='owner' />
    <InputField label='New task: ' @addTaskFromInput="addTask" />
    <TaskList randoproperty="This is a randomly parsed property" :taskList="todoList" />
    <p><button @click="eraseAll">Clear all</button></p>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'
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
  owner = 'Emkyo'
  todoList = [
    {
      name: 'Learn Elm',
      done: false
    },
    {
      name: 'Play Pico-8',
      done: false
    },
    {
      name: 'Watch StarCraft',
      done: true
    }
  ]

  mounted () {
    // load localstorage
    if (localStorage.owner) {
      this.owner = localStorage.owner
    }
    if (localStorage.todoList) {
      this.todoList = JSON.parse(localStorage.todoList)
    }

    // Component to component communication via bus event
    this.$root.$on('updateOwner', (_owner: string) => {
      this.owner = _owner
    })

    this.$root.$on('deleteTask', (_index: number) => {
      // console.log('index to be deleted: ' + _index.toString())
      this.todoList.splice(_index, 1)
    })

    this.$root.$on('updateListCompletion', (_index: number, _done: boolean) => {
      this.todoList[_index].done = _done
      // console.log(_index + _done.toString())
    })

    this.$root.$on('pushTaskToTheEnd', (_index: number) => {
      // console.log(_index)
      const tempTask = this.todoList[_index]
      this.todoList.splice(_index, 1)
      this.todoList.push(tempTask)
    })
  }

  // Child to parent communication via event listening
  addTask (taskName: string) {
    this.todoList.unshift({ name: taskName, done: false })
  }
  // One more method of child to parent communication not implemented here

  eraseAll () {
    this.todoList = []
  }

  @Watch('owner')
  ownerChanged (_newOwner: string) {
    localStorage.owner = _newOwner
  }

  @Watch('todoList')
  todoListChanged (_newTodoList: Array<{ name: string; done: boolean }>) {
    localStorage.todoList = JSON.stringify(_newTodoList)
    // console.log(JSON.stringify(_newTodoList))
  }
}

</script>

<style lang="scss">

$font-fam: "Roboto Condensed", Helvetica, sans-serif;

#app {
  font-family: $font-fam;
  font-weight: 300;
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
  // background-image: linear-gradient(20deg, #111 80%, #edfd88 20% )
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
  transition-duration: 0.2s;
}

button:focus {
  outline: #4DB6AC auto 1px;
}

button:hover {
  color: #eee;
}

</style>
