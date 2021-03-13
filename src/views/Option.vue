<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h2>You have xxx</h2>
    <div v-if="!isEditing">
      <input
        placeholder="add todo"
        @keyup.enter="addTodo"
        v-model="newTodoName"
        type="text"
      />
    </div>
    <div  v-else>
      <input
        placeholder="add todo"
        @keyup.enter="updateTodo"
        v-model="newTodoName"
      />
    </div>
    <div class="todos">
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{todo.name}}</span>
          <button @click="editTodo(index, todo.name)">edit</button>
          <button @click="deleteTodo(index)">x</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  data() {
    return {
      isEditing: false,
      selectedIndex: null,
      newTodoName: '',
      todos: [
        {
          id: 1,
          name: "one",
        },
        {
          id: 2,
          name: "two",
        },
        {
          id: 3,
          name: "three",
        },
      ],
    };
  },
  methods: {
    addTodo() {
      let newTodo = {
        id: Date.now(),
        name: this.newTodoName
      }
      console.log(newTodo)
      this.todos.push(newTodo);
      this.newTodoName= ''
    },

    editTodo(index,todo){
      console.log(index,todo);
      this.isEditing = true;
      this.newTodoName = todo;
      this.selectedIndex = index;
    },

    updateTodo() {
      let newTodo = {
        id: Date.now(),
        name: this.newTodoName
      }
      this.todos.splice(this.selectedIndex, 1, newTodo);
      this.newTodoName = "";
      this.isEditing = false;
    },

    deleteTodo(index) {
      this.todos.splice(index, 1)
    }
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}
li {
  border: 1px solid;
  margin-bottom: 10px;
  display: flex;
}
li span {
  flex-grow: 1;
}
</style>
