<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">
          Simple todo app
        </h5>
        <div class="row">
          <div class="col-10">
            <input v-model="todo" type="text" class="form-control" @keyup.enter="add">
          </div>
          <div class="col-2">
            <button class="btn btn-success" @click="add">ADD</button>
          </div>
        </div>
        
      </div>
      <List :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo"/>
      <span>total: {{ total }}</span>
    </div>
  </div>
</template>

<script>
import List from './components/List.vue';
export default {
  components: {
    List
  },
  data() {
    return {
      todo: "",
      todos: []
    }
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  computed: {
    total() {
      return this.todos.length;
    }
  },
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false,
      });
      this.todo = "";
      this.saveToLocalStorage();
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if(index != todoIndex){
          return item
        }
      })
      this.saveToLocalStorage();
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if(index == todoIndex) {
          item.isDone = true;
        }

        return item;
      })
      this.saveToLocalStorage();
    },
    saveToLocalStorage() {
      localStorage.setItem('todos', JSON.stringify(this.todos));
    }
  },
}
</script>

