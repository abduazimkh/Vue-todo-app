
<script>
  export default {
    name: "NewTask",
    components: "",
    props: {},
    data() {
      return {
        task: {
          newTaskTitle: "",
          newTaskDesc: ""
        }
      };
    },
    methods: {
    },
    computed: {}
  };
</script>

<template>
  <div class="new-task">
      <h3>Add a new task</h3>
    <div class="input-item" @keyup.enter="$emit('create-new-task', task)">
      <input type="text" placeholder="Enter a task name" v-model="task.newTaskTitle" />
      <input type="text" placeholder="Enter a task description" v-model="task.newTaskDesc" />
    </div>
    <button @click="$emit('create-new-task', task)">Add Todo</button>
  </div>
</template>



<style>
  .new-task{
    display: flex;
    flex-direction: column;
    gap: 1rem;
    padding: 0 1rem 1rem 1rem;
    h3{
      font-size: 1.5rem;
      color: #fff;
    }

    .input-item{
      display: flex;
      align-content: center;
      height: 40px;
      gap: 1rem;
      input{
        flex: 1;
        font-size: 1rem;
        text-indent: 1rem;
        outline: none;
        border: 1px solid transparent;

        &:focus{
          border: 1px solid orange;
          box-shadow: 0 0 5px 1px red;
        }
      }
    }

    button{
      background-color: blueviolet;
      color: #fff;
      font-size: 1rem;
      padding: .8rem 1rem;
      border: none;
    }
  }
</style>
