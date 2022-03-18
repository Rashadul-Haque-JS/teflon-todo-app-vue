<template>
  <div>
    <li class="todo-task">
      <input
        for="task"
        type="checkbox"
        v-model="task.done"
        class="task-check"
      />
      <label for="task" class="task-feild">{{ task.content }}</label>
      <img src="../assets/delete.svg" alt="delete icon" @click="deleteTask()" />
    </li>
  </div>
</template>

<script>
export default {
    
  props: ["task"],
  data() {
    return {
      textClr: 10,
    };
  },

  computed: {
    className() {
      let classes = ["toggle"];
      if (this.task.done) {
        classes.push("toggle-done");
      }
      return classes;
    },
  },

  methods: {
    deleteTask(index) {
      this.$emit("delete", index);
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@200;300;600;700&display=swap");

.todo-task {
  display: flex;
  align-items: center;
  position: relative;
  padding: 12px 0px;
  background-color: #b6b3b3e5;
  list-style-type: none;
  margin: 5px 0px;
  font-family: "Titillium Web", sans-serif;
  font-weight: 600;
}

input[type="checkbox"] {
  margin: 0px 15px 0px 10px;
  width: 2.15em;
  height: 2.15em;
  
}

.todo-task img {
  position: absolute;
  right: 20px;
  cursor: pointer;
}
.todo-task img:hover {
  transform: translateY(-1px);
}

.task-check:checked + .task-feild {
  text-decoration: line-through;
  opacity: 0.4;
  
}
</style>