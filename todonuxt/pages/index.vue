<template>
  <main>
    <h1>Task Board</h1>
    <p>Create a list of tasks</p>

    <div class="create-new">
      <form @submit.prevent="addTodo">
        <input type="text" v-model="todoName" placeholder="Add a new task" />
        <button>Submit</button>
      </form>
    </div>

    <div class="tasks">
      <div class="content" v-for="(todo, index) in todos" :key="index">
        <div class="task" :class="`${todo.completed ? 'is-complete' : ''}`">
          <!-- {{ index + 1 }}. {{ todo.name }} - {{ todo.completed }} -->
          {{ index + 1 }}. {{ todo.name }}

          <div class="buttons">
            <button @click="completeTodo(todo)">
              {{ todo.completed ? "Undo" : "Done" }}
            </button>

            <button @click="removeTodo(index)" class="delete">Delete</button>
          </div>
        </div>
      </div>
    </div>

    <!-- <div class="tasks">
      <Task v-for="(todo, index) in todos" :key="index" :todos="todos"> </Task>
    </div> -->
  </main>
</template>

<script lang="ts" setup>
import { TodoItem } from "~~/types/todo";

const todos = useState("todos", () => [] as TodoItem[]);

const todoName = ref("");

const addTodo = () => {
  todos.value.push({
    name: todoName.value,
    completed: false,
  });
  todoName.value = "";
};

function removeTodo(index) {
  todos.value.splice(index, 1);
}
function completeTodo(todo) {
  todo.completed = !todo.completed;
}
</script>


