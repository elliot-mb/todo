<!-- run this app locally https://youtu.be/WmrawkHYMTg?t=121 -->

<template>
  <div>

    <strong>Things to do</strong>

    <form v-on:submit.prevent="doneTodo">
      <ul>
        <li v-for="(todo, index) in todos" v-bind:key="todo">
          <button id="x-button" type="submit" v-on:click="doneIndex=index">X</button>
          {{ todo }}
        </li>
      </ul>
    </form>

    <form v-on:submit.prevent="addTodo">
      <input v-model="todoText" placeholder="What needs to be done?"> <!-- vue-model directive binds input todoText to form input value -->
      <button type="submit" v-if="todoText != ''">Add Todo</button>
    </form>

  <button v-on:click.prevent="clearTodo">Clear all Todos</button>

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
      this.todos = [...this.todos, this.todoText]; //appends todoText of element to array
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
  color: purple;
}

li{
  list-style-type: none;
  padding-right: 35px;
}

</style>
