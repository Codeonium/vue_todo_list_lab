<template>
  <div id="app">
    <h1>ToDo List</h1>
    <form v-on:submit.prevent="saveNewTask">
      <label for="new-task">Enter a task: </label>
      <input type="text" id="new-task" v-model="newTask.name" required>

      <span>
        <input type="radio" name="priority" id="high" value="high" v-model="newTask.priority" required>
        <label for="high">High</label>
      </span>
      <span>
        <input type="radio" name="priority" id="low" value="low" v-model="newTask.priority" required>
        <label for="low">Low</label>
      </span>

      <input type="submit" value="Add task">
    </form>
    <ul>
      <li v-for="item, index in todoList" v-bind:key="index" v-bind:class="item.priority">
        <span v-bind:class="item.isDone ? 'done' : 'notDone'">{{item.name}}</span>
      
        <button v-if="item.priority === 'low'" @click="changePriorityLow(index)">Make High Priority</button>
        <button v-else @click="changePriorityHigh(index)">Make Low Priority</button>

        <button v-if="!item.isDone === true" @click="changeToDone(index)">Done</button>
        <button v-else @click="changeToNotDone(index)">Undo</button>

      </li>
    </ul>
  </div>
</template>

<script>


export default {
  name: 'App',
    data() {
      return {
        todoList: [
          {name: "Clean the Kitchen" , priority: "low", isDone: false},
          {name: "Walk the Dog", priority: "high", isDone: true},
          {name: "Finish the MVP", priority: "low", isDone: false}
        ],
        newTask: {name: "", priority: null, isDone: false}
      }
    },
    methods: {
      saveNewTask: function() {
        this.todoList.push(this.newTask),
        this.newTask = {name: "", priority: null, isDone: false}
      },
      changePriorityLow(index){
        this.todoList[index].priority = "high";
      },
      changePriorityHigh(index){
        this.todoList[index].priority = "low";
      },
      changeToDone(index){
        this.todoList[index].isDone = true;
      },
      changeToNotDone(index){
        this.todoList[index].isDone = false;
      }

    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: pink;
}
ul {
  list-style: none;
  max-width: 500px;
  margin: auto;
}
li {
  margin: 10px 0 10px 0;
  padding: 20px;
}
button {
  margin: 10px;
  padding: 15px;
  border: solid 2px lightcoral;
  border-top: solid 2px blue ;
  border-bottom: solid 2px green;
  border-radius: 30px;
  color: black;
  background-color: lightgoldenrodyellow;
}
input {
  background-color: lightgoldenrodyellow;
}
.low .notDone {
  border: solid 3px green;
  border-radius: 30px;
  background-color: rgba(0, 128, 0, 0.06);
  padding: 10px;
  /* text-decoration: none; */
}
.high .notDone {
  border: solid 3px red;
  border-radius: 30px;
  background-color: rgba(255, 0, 0, 0.06);
  padding: 10px;
  /* text-decoration: none; */
}
.done {
  color: grey;
  background-color: rgba(121, 121, 121, 0.06);
  padding: 10px;
  text-decoration: wavy line-through;
}
</style>
