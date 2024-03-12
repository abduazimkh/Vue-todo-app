<script>
  import TaskItem from "./TaskItem.vue";
  import NewTask from "./NewTask.vue";

export default {
    name: "TodoList",
    components: { NewTask, TaskItem },
    data() {
      return {
        tasks: [],
        filterBy: "all"
      };
    },
    mounted() {
      this.getFromLocalStorage();
    },
    methods: {
      createNewTask(task) {
        let newTask = {
          taskTitle: task.newTaskTitle,
          taskDescription: task.newTaskDesc,
          taskStatus: "todo",
          taskId: this.newTaskId
        };
        if (newTask.taskTitle.length > 0) {
          this.tasks.push(newTask);
          this.saveToLocalStorage();
        }
      },
      updateATask(updatedTask) {
        this.tasks.forEach(task => {
          if (task.taskId === updatedTask.itemId) {
            task.taskTitle = updatedTask.itemTitle;
            task.taskDescription = updatedTask.itemDesc;
            task.taskStatus = updatedTask.itemStatus;
          }
        });
        this.saveToLocalStorage();
      },
      getFromLocalStorage() {
        if (localStorage.tasks) this.tasks = JSON.parse(localStorage.getItem("tasks"));
      },
      saveToLocalStorage() {
        localStorage.setItem("tasks",JSON.stringify(this.tasks));
      },
    },
    computed: {
      newTaskId() {
        return (
          this.tasks.reduce((max, curr) => Math.max(max, curr.taskId), 0) + 1
        );
      },
      tasksToShow() {
        return this.filterBy === "all"
          ? this.tasks.filter(task => task.taskStatus !== "deleted")
          : this.tasks.filter(task => task.taskStatus === this.filterBy);
      }
    }
  };
</script>


<template>
  <div class="todo__wrapper">
    <div class="filter-bar">
      <button @click="filterBy = 'all'">all</button>
      <button @click="filterBy = 'todo'">todo</button>
      <button @click="filterBy = 'done'">done</button>
    </div>
    <new-task @create-new-task="createNewTask"></new-task>
    <div class="task--list">
      <div v-for="task in tasksToShow" :key="task.taskId">
      <task-item
        class="blue"
        :task-details="task"
        @task-update="updateATask"
      ></task-item>
      </div>
    </div>
  </div>
</template>



<style scoped>
  .todo__wrapper{
    background-color: #333;

  }
  .filter-bar{
    display: flex;
    justify-content: space-around;
    padding: 1rem 0;
    button{
      padding: .7rem 1rem;
      font-size: 1rem;
      color: #fff;
      border: none;
      transition: .1s ease;
      min-width: 70px;
      &:active{
        transform: scale(.97);
      }
      &:first-child{
        background-color: dodgerblue;
      }
      &:nth-child(2){
        background-color: orange;
      }
      &:nth-child(3){
        background-color: grey;
      }
    }
  }
  .task--list{
    border-top: 1px solid #fff;
    max-height: 415px;
    min-height: 415px;
    overflow-y: auto;
    background-color: #333;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
    &::-webkit-scrollbar{
      display: none;
    }
  }

  .blue {
    min-height: 100px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    background-color: #fff;

  }
</style>
