<template>
  <div id="app">
    <header>
      <nav class="navbar">
        <img src="./assets/menu.svg" alt="menu icon" @click="showThisMenu" />
        <TodoMenu
          :show="showMenu"
          :taskArray="savedDone"
          @close="hideMenu()"
          @clear="emptyStorage"
          :hide="hidden"
          @hideIt="hideList()"
        />
      </nav>

      <div class="headlines">
        <img src="./assets/teflon-panna.svg" alt="panna" />
        <h1>TEFLON</h1>
        <p>När det inte fastnar</p>
      </div>
    </header>
    <main class="main-division">
      <p>Du har {{ array.length }} kvar att göra</p>
      <TodoList v-bind:arr="array" @deleteIt="deleted" />
    </main>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import TodoMenu from "./components/TodoMenu.vue";

export default {
  data() {
    return {
      array: [{ id: 1, content: "Todo-1", done: false }],
      savedDone: [],
      showMenu: false,
      hidden: false,
    };
  },
  components: {
    TodoList,
    TodoMenu,
  },
  methods: {
    deleted(index) {
      this.array.splice(index, 1);
    },

    hideMenu() {
      this.showMenu = !this.showMenu;
    },
    showThisMenu() {
      this.showMenu = !this.showMenu;
    },
    hideList() {
      this.hidden = !this.hidden;
    },
    emptyStorage() {
      localStorage.clear();
    },
    loadLocalStorageData() {
      let listArray;
      if (localStorage.getItem("arr")) {
        listArray = JSON.parse(localStorage.getItem("arr"));
      }
      listArray.forEach((e) => {
        if (e.done == true) {
          this.savedDone.push(e);
        }
      });
    },
    addTask() {
      this.array.push({ id: this.array.length + 1, content: this.task, done: false });
      this.task = ""; 
      this.saveDataToLocalStorage();
    },
    saveDataToLocalStorage() {
      localStorage.setItem("arr", JSON.stringify(this.array));
    },
  },
  watch: {
    array: {
      handler() {
        this.saveDataToLocalStorage();
      },
      deep: true,
    },
  },
  mounted() {
    this.loadLocalStorageData();
    window.addEventListener("storage", () => {
      this.loadLocalStorageData();
    });
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:wght@200;300;600;700&display=swap");

* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

#app {
  display: grid;
  grid-template-columns: 1fr;
  width: 360px;
  position: relative;
  margin: 30px auto 0px auto;
  padding: 5px 10px 16px 10px;
  background-color: #f2f2f2;
  font-family: "Titillium Web", sans-serif;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

.navbar {
  width: 100%;
  padding: 5px 0px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.navbar img {
  margin-right: 20px;

  cursor: pointer;
}

.headlines {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
}

.headlines img {
  margin-left: 20px;
}

.headlines h1 {
  line-height: 40px;
  font-size: 2.2rem;
  font-weight: 700;
  margin: 0px;
}

.headlines p {
  font-size: 0.7rem;
  font-weight: 600;
  text-align: center;
  margin-top: 0px;
}

.main-division {
  margin: 55px 0px 0px 0px;
  padding-bottom: 8px;
}

.main-division p {
  text-align: center;
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 20px;
}
</style>
