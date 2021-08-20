<!-- run this app locally https://youtu.be/WmrawkHYMTg?t=121 -->

<template>
  <div>

    <h1 id="heading">Things to do</h1>

    <div class="todo">
      <form v-on:submit.prevent="doneTodo">
        <ul>
          <li v-for="(todo, index) in todos" v-bind:key="todo">
            <button id="x-button" type="submit" v-on:click="doneIndex=index">X</button>
            {{ todo }}
          </li>
        </ul>
      </form>
    </div>

    <div class="entry-box">
      <form v-on:submit.prevent="addTodo">
        <input v-model="todoText" placeholder="What needs to be done?"> <!-- vue-model directive binds input todoText to form input value -->
        <button class="text-button" type="submit" v-if="todoText != ''">Add Todo</button>
        <button class="text-button" id="greyed" v-if="todoText == ''" disabled>Add Todo</button>
      </form>

      <button class="text-button" id="clear" v-on:click.prevent="clearTodo">Clear all Todos</button>
    </div>

  </div>
</template>

<script> //component represented as a plain javascript object (POJO) like a class but plain and boring
export default{
  name: "HelloWorld", //reactive data or state
  data: function(){
    return{
      todos:[],
      todoText:'',
      doneIndex:0,
    };
  },
  methods: { //to change the state of this object
    addTodo: function(){
      this.todos = [...this.todos, `> ${this.todoText}`]; //appends todoText of element to array
      this.todoText = '';
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    doneTodo: function(){
      this.todos.splice(this.doneIndex, 1);
      localStorage.setItem('todos', JSON.stringify(this.todos));
    },
    clearTodo: function(){
      this.todos = [];
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  },
  mounted: function(){
    const existingTodos = localStorage.getItem('todos');
    this.todos = JSON.parse(existingTodos) || [];
  }
};
</script>

<style scoped>

#x-button{
  padding: 0;
  border: none;
  background: none;
  color: red;
  display: none;
}

#heading{
  font-size: 1.5em;
  margin-top: -40px;
  padding: 15px;
}

#clear{
  float: right;
  margin-top: 10px;
  margin-right: 1px;
  background: #ffdddd;
  border-radius: 5px;
}

#greyed{
  color: #aaaaaa;
}

.text-button{
  padding: 5px;
}

li{
  list-style-type: none;
  padding: 7px;
  color: #666666;
}

li:hover{
  color: #000000;
  margin-left: -13.5px;
}

li:hover #x-button{
  display: inline;
  font-weight: bolder;
}

#x-button:hover{
  display: inline;
}

input{
  width: calc(50vw - 184px);
  padding: 5px;
}

.todo{
  text-align: left;
  margin-left: 25vw;
  margin-right: 25vw;
  margin-top: 10px;
  padding: 18px 45px 27.5px 0;
  height: calc(100vh - 300px);
  background-color: #ddeeff;
  overflow: auto;
  border-radius: 10px;
}

.entry-box{
  position: fixed;
  bottom: 0;
  margin: 0 0 0 25vw;
  padding: 40px 40px 20px;
  width: calc(50vw - 96px);
  background: #dddddd;
  text-align: left;
  border-radius: 10px;
}

</style>
