<template>
  <div class="first">
    <div class="all">
      <CookieContent> </CookieContent>
      <div>
        <img class="pic" :src="require('./Todo_logo.png')" alt="" />
        <p class="p1">Checklista</p>
      </div>
      <p>Du har {{ tasksLeftToDo }} todos kvar att göra</p>
      <div class="wrapper">
        <div class="ul">
          <List
            v-for="(task, id) in todolista"
            :key="id"
            :element="task"
            @remove-element="removeElement(task.id)"
            @checked-tasks="checked(task)"
          />
          <form @submit.prevent="clickHandler" class="form">
            <input
              class="input"
              type="text"
              v-model="field"
              @keydown.enter="clickHandler"
            />
            <button type="button" @click="clickHandler" class="button">
              LÄGG TILL TODO
            </button>
            <p v-if="error">Måste innehålla mer än 2 tecken</p>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import List from "./lista";
import CookieContent from "./cookie-content";

export default {
  components: { List, CookieContent },

  data() {
    return {
      field: "",
      todolista: [],
      error: false,
    };
  },
  computed: {
    tasksLeftToDo() {
      return this.todolista.filter((task) => task.isDone === false).length;
    },
  },

  methods: {
    clickHandler() {
      if (this.field.length < 3) {
        this.error = true;
        this.field = "";
      } else {
        this.addThing(this.field);
        this.field = "";
        this.error = false;
      }
    },
    addThing(task) {
      const newThing = {
        id: new Date().toISOString(),
        name: task,
        isDone: false,
      };
      return this.todolista.push(newThing);
    },
    checked(theTodo) {
      theTodo.isDone = !theTodo.isDone;
    },

    removeElement(id) {
      this.todolista = this.todolista.filter((thing) => thing.id !== id);
    },
  },
};
</script>

<style>
.first {
  display: flex;
  justify-content: center;
  margin-top: 8%;
  margin-bottom: 8%;
  margin-right: 10%;
  margin-left: 10%;
  font-family: "Open Sans", sans-serif;
}

.all {
  box-shadow: 8px 10px 17px 1px rgba(160, 218, 157, 0.91);
  max-width: 80%;
  padding: 20px;
  justify-content: center;
  text-align: center;
}
.pic {
  width: 40%;
  margin-bottom: 30px;
  padding-top: 20px;
}
.p1 {
  margin-top: unset;
  font-weight: 800;
  color: #a0da9d;
  font-size: 30px;
}
.form {
  padding: 5px;
  display: flex;
  margin: auto;
  flex-direction: column;
  width: 300px;
}
.input {
  width: 300px;
  height: 40px;
  margin: auto;
  border: solid #a0da9d;
  font-size: 17px;
}
.input:focus,
.input:active {
  outline: none;
  background-color: #f0f8ef;
}
.button {
  width: 310px;
  margin: auto;
  height: 50px;
  background-color: #a0da9d;
  border: thick;
  color: white;
  font-size: 20px;
  cursor: pointer;
  outline: none;
}
.button:hover,
.button:active {
  width: 310px;
  margin: auto;
  height: 50px;
  background-color: #5ca15c;
  border: thick;
  color: white;
  font-size: 20px;
  cursor: pointer;
  outline: none;
}
.wrapper {
  display: grid;
  grid-template-columns: 80%;
  justify-content: center;
}
.ul {
  list-style: none;
  padding: 0;
  font-weight: 500;
  font-size: 20px;
  align-items: center;
}
</style>
