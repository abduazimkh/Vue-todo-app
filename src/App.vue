<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "app",
  components: {
    TodoList
  }
};
</script>

<template>
  <div id="app">
    <div class="todo-app">
      <h2>My little to do list</h2>
      <todo-list />
    </div>
  </div>
</template>

<style>
#app {
  width: 100%;
  height: 100vh;
  background-color: #0009;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
}

.todo-app{
  max-width: 900px;
  width: 100%;
  max-height: 750px;
  height: 100%;
  overflow-y: hidden;
  background-color: #fff;
  padding: 1rem;
  h2{
    text-align: center;
    color: orangered;
    font-size: 3rem;
    margin-bottom: 1rem;
  }

}

</style>
