<template>
  <header class=" container ml-auto mr-auto sticky top-0 z-20 flex items-center justify-between border-b bg-white p-3">
    <a href="#">
      <img src="./assets/logo.svg" alt="logo" class=" h-6">
    </a>
    <a href="#">
      <div class=" flex items-center gap-1">
        <div class="h-7 w-7 rounded-full bg-green-500"></div>
      </div>
    </a>
  </header>
  <main class="flex flex-col items-center  pt-10">
    <div id="app" class=" w-2/4">
      <h1 class=" my-4 text-3xl text-center">Список задач</h1>
      <todo-form @todo-added="addTodo"></todo-form>
      <ul class="border border-green-500 p-4 rounded-b-md border-t-0">
        <li class=" p-2 border-b border-green-500 flex justify-between text-black" v-for="item in todoItems"
          :key="item.id">

          <to-do-item :label="item.label" :date="item.date" :id="item.id" @item-deleted="deleteTodo(item.id)"
            @item-edited="editTodo(item.id, $event)">
          </to-do-item>

        </li>
      </ul>
    </div>
  </main>
</template>
<script>
import ToDoItem from "./components/TodoItem.vue";
import TodoForm from './components/TodoForm.vue'
import Id from "lodash.uniqueid";
export default {
  name: "app",
  components: {
    TodoForm,
    ToDoItem
  },

  data() {
    return {
      todoItems: [
        { id: Id(), label: "Закончить проект", date: '2.08.2023' },
        { id: Id(), label: "Изучить Vue", date: '2.08.2023' },
        { id: Id(), label: "Создать Список задач", date: '2.08.2023' },
        { id: Id(), label: "Начать работать", date: '15.08.2023' },
      ]
    };
          
  },
  mounted(){
    const local = localStorage.getItem('todo')
    console.log("local", local);
   local ? this.todoItems = JSON.parse(local) : null

  },
  methods: {
    
    addTodo(todoLabel) {
      const current = new Date();
      const date = `${current.getDate()}.${current.getMonth() + 1}.${current.getFullYear()} / ${current.getHours()}: ${current.getMinutes()} :${current.getSeconds()}`;
      this.todoItems.push({ id: Id(), label: todoLabel, date: date })
      localStorage.setItem('todo',JSON.stringify(this.todoItems))
    },
    deleteTodo(todoId) {
      const itemIndex = this.todoItems.findIndex((item) => item.id === todoId);
      this.todoItems.splice(itemIndex, 1);
      localStorage.setItem('todo',JSON.stringify(this.todoItems))

    },
    editTodo(todoId, newLabel) {
      const toDoToEdit = this.todoItems.find((item) => item.id === todoId);
      toDoToEdit.label = newLabel;
      localStorage.setItem('todo',JSON.stringify(this.todoItems))

    },

  }
}
</script>