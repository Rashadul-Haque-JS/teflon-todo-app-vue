<template>
  <div>
    <TodoTask
      v-for="(task, index) in arr"
      :key="task.id"
      :task="task"
      :index="index"
      @delete="deleteItem(index)"
    />
    <div class="add-to-list">
      <input type="text" v-model="task" />
      <button class="btn" @click="addTask">Lägg till todo</button>
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
    },

    deleteItem(index) {
      this.$emit("deleteIt", index);
    },
    //  isDone(){
    //      this.$emit('done')
    //  }
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@200;300;600;700&display=swap");

.add-to-list {
  display: flex;
  flex-direction: column;
  margin-top: 20px;
}

input[type="text"],
.btn {
  padding: 18px 0px;
}
.btn {
  background-color: #000;
  color: #fff;
  font-family: "Titillium Web", sans-serif;
  font-size: 1rem;
  font-weight: 600;
}
</style>