<template>
  <div class="todo-menu " v-if="show">
    <img class="close-menu" src="../assets/close.svg" alt="close icon" @click="closeMenu"/>
    <div class="hide-del-clear hide"  @click="hideDone">
      <img src="../assets/visibility.svg" alt="visibilty icon" />
      <p>Hide done todos</p>
    </div>
    <div v-if="!hide">
    <li class="todo-task" v-for="obj in taskArray" :key="obj.id">
        <span class="task-done">✔ &#160;{{obj.content}}</span>
    </li>
    </div>
    <div class="hide-del-clear delete">
      <img src="../assets/delete.svg" alt="delete icon" />
      <p>Delete done todos</p>
    </div>
    <div class="hide-del-clear clear-all" @click="clearAll">
      <img src="../assets/delete_forever.svg" alt="delete forever icon" />
      <p>Clear all data</p>
    </div>
  </div>
</template>

<script>
export default {
    name:'todoMenu',
    props: {show:Boolean, taskArray:Array, hide:Boolean},
    methods: {
      closeMenu() {
        this.$emit("close");
      },
      clearAll(){
        this.$emit('clear')
      },
       hideDone(){
      this.$emit('hideIt')
    }
    },
   
};
</script>

<style  scoped>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@200;300;600;700&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.todo-menu {
  display: flex;
  flex-direction: column;
  width: 320px;
  background-color: #fff;
  position: absolute;

  top: 0;
  right: 0;
  bottom: 0;
  box-shadow: -3px 2px 33px 18px rgba(0, 0, 0, 0.1);
  z-index: 1;
}


.todo-menu .close-menu {
  align-self: flex-end;
  margin: 8px 8px 30px 0px;
  cursor: pointer;
}

.todo-menu .hide-del-clear {
  display: flex;
  width: 100%;
  padding: 15px;
  font-family: "Titillium Web", sans-serif;
  font-weight: 600;
}
.todo-menu .hide-del-clear p {
  width: fit-content;
  text-align: start;
  margin-left: 10px;
}

.hide,
.delete {
  margin: 10px 0px;
  background-color: #f5f1f1;
  cursor:pointer
}

.todo-task {
  text-align: center;
  padding: 8px 0px;
  background-color: #bde07ce5;
  list-style-type: none;
  font-family: "Titillium Web", sans-serif;
  font-weight: 600;
  margin: 5px 0px;
}

.clear-all {
  /* transform: translateY(120px); */
  background-color: #ffb3b2;
  position: sticky;
  bottom: 5px;
  cursor:pointer;
}
</style>