<script>
export default {
  name: "TaskItem",
  props: {
    taskDetails: {
      taskTitle: String,
      taskDescription: String,
      taskStatus: String,
      taskId: Number
    }
  },
  data() {
    return {
      showDescription: false,
      editDescription: false,
      editTitle: false,
      task: {
        itemTitle: this.taskDetails.taskTitle,
        itemDesc: this.taskDetails.taskDescription,
        itemStatus: this.taskDetails.taskStatus,
        itemId: this.taskDetails.taskId
      }
    };
  },
  methods: {
    setStatusButton() {
      this.task.itemStatus = this.task.itemStatus === "todo" ? "done" : "todo";
    },
    moveToDeleted() {
      this.task.itemStatus = "deleted";
    }
  },
  updated() {
    this.$emit("task-update", this.task);
  },
  computed: {
    editTitleButton() {
      return this.editTitle ? "save" : "edit";
    },
    editDescriptionButton() {
      return this.editDescription ? "save" : "edit";
    },
    statusButton() {
      return this.task.itemStatus === "todo" ? "Done" : "Todo";
    }
  }
};
</script>


<template>
  <div class="todo__item--content">
    <div class="todo__edit--box">
      <div class="todo__edit--items">
        <div class="clickable" @click="showDescription = !showDescription">
          <input
            class="clickable"
            :disabled="!editTitle"
            type="text"
            v-model="task.itemTitle"
            @blur.stop="editTitle = false"
          />
        </div>
        <button v-show="!showDescription" @click="editTitle = !editTitle">
          {{ editTitleButton }}
        </button>
      </div>
    </div>
    <div v-show="showDescription">
      <textarea
        :disabled="!editDescription"
        v-model="task.itemDesc"
        @blur.stop="editDescription = false"
      ></textarea>
    </div>
    <p>
    {{ task.itemStatus }}
    </p>
    <button
      v-show="showDescription"
      @click="editDescription =! editDescription"
    >
      {{ editDescriptionButton }}
    </button>
    <button class="status-btn" @click="setStatusButton">{{ statusButton }}</button>
    <button class="delete-btn" @click="moveToDeleted">Delete</button>
  </div>
</template>


<style scoped>

  .todo__item--content{
    textarea{
      resize: none;

      &::-webkit-scrollbar{
        display: none;
      }
    }
    p{
      border: 1px solid #111;
      width: 70px;
      height: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    button{
      background-color: #111;
      height: 30px;
      width: 70px;
      color: #fff;
      font-size: 1rem;
      border: none;
      transition: all .3s ease;
      &:active{
        transform: scale(.97);
      }
    }
    .status-btn{
      background-color: dodgerblue;
    }
    .delete-btn{
      background-color: red;
    }
  }

  .todo__edit--items{
    display: flex;
    align-items: center;
    gap: 1rem;
    input{
      text-indent: 10px;
      height: 30px;
    }
    button{
      background-color: orangered;
    }
  }


.clickable {
  cursor: pointer;
}


</style>
