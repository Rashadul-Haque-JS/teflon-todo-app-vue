<template>
  <div>
    <div class="task-wrapper">
      <TodoTask
        v-for="(task, index) in arr"
        :key="task.id"
        :task="task"
        :index="index"
        @delete="deleteItem(index)"
      />
    </div>
    <div class="add-to-list">
      <input type="text" v-model="task" class="task-input" placeholder="Skriv ny todo" />
      <button class="btn" @click="addTask">LÄGG TILL TODO</button>
    </div>
  </div>
</template>

<script>
import TodoTask from "./TodoTask.vue";
export default {
  data() {
    return {
      task: "",
    };
  },
  name: "todoList",
  props: ["arr"],
  components: {
    TodoTask,
  },
  computed: {
    add() {
      return {
        id: this.arr.length + 1,
        content: this.task,
        done: false,
      };
    },
  },
  methods: {
    addTask() {
      this.arr.push(this.add);
      this.task = ""; // Clear the input field after adding the task
    },
    deleteItem(index) {
      this.$emit("deleteIt", index);
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@200;300;600;700&display=swap");

.task-wrapper {
  min-height: 100px;
  max-height: 140px;
  overflow-y: auto;
}
.add-to-list {
  display: flex;
  flex-direction: column;
  margin: 20px 10px;  
}

input[type="text"] {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-family: "Titillium Web", sans-serif;
  font-size: 1rem;
  margin-bottom: 10px;
}

.btn {
  padding: 10px 20px;
  background-color: #337ab7;
  color: #fff;
  font-family: "Titillium Web", sans-serif;
  font-size: 1rem;
  font-weight: 600;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.btn:hover {
  background-color: #23527c;
}
</style>
