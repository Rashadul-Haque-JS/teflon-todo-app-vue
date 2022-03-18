<template>
  <div id="app">
    <header>
      <nav class="navbar">
        <img src="./assets/menu.svg" alt="menu icon" @click="showThisMenu" />
        <TodoMenu :show="showMenu" :taskArray="savedDone" @close="hideMenu()" @clear="emptyStorage" :hide="hidden" @hideIt="hideList()"/>
      </nav>

      <div class="headlines">
        <img src="./assets/teflon-panna.svg" alt="panna" />
        <h1>TEFLON</h1>
        <p>När det inte fastner</p>
      </div>
    </header>
    <main class="main-division">
      <p>Du har {{ array.length }} kvar todo att göra</p>
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
      array: [
        { id: 1, content: "Todo-1", done: false },
      ],

      // Att testa menus layout....
      savedDone: [
        
      ],

      showMenu: false,
      hidden:false
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
      this.showMenu == false ? this.showMenu = true : this.showMenu = false;
     
    },
    showThisMenu() {
      this.showMenu == false ? this.showMenu = true : this.showMenu = false;
    },
    hideList(){
      this.hidden == false ? this.hidden = true : this.hidden = false;
    
    },
    emptyStorage(){
      localStorage.clear()
    }
  },
  // mounted() {
  //   if (localStorage.getItem("arr")) {
  //     this.array = JSON.parse(localStorage.getItem("arr"));
  //   }
  // },

  watch: {
    array: {
      handler() {
        localStorage.setItem("arr", JSON.stringify(this.array));
      },
      deep: true,
    },
  },
  created() {
    let listArray;
    if (localStorage.getItem("arr")) {
    listArray = JSON.parse(localStorage.getItem("arr"));
    }
    listArray.map((e)=>{
      if (e.done==true){
        this.savedDone.push(e)
        console.log(this.savedDone);
      }
    })
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
  padding: 5px 10px;
  background-color: #fff;
  font-family: "Titillium Web", sans-serif;
  box-shadow: -3px 4px 33px 18px rgba(0, 0, 0, 0.1);
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

  margin: 0px 0px;
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