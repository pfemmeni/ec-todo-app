<template>
  <div class="first">
    <div class="all">
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
            :element="task.name"
            :id="task.id"
            :task-is-done="task.isDone"
            @remove-element="removeElement"
            @checked-tasks="checked"
          />
        </div>
      </div>

      <form @submit.prevent="clickHandler" class="form">
        <input
          class="input"
          type="text"
          v-model="field"
          @keydown.enter.="clickHandler"
        />
        <button type="button" @click="clickHandler" class="button">
          LÄGG TILL TODO
        </button>
        <p v-if="error">Måste innehålla mer än 2 tecken</p>
      </form>
    </div>
  </div>
</template>

<script>
import List from "./lista";
export default {
  components: { List },

  data() {
    return {
      field: "",
      todolista: [],
      error: false,
      tasksLeftToDo: 0,
    };
  },

  methods: {
    tasksLeft() {
      for (this.task in this.todolista) {
        if (!this.task.isDone) {
          this.tasksLeftToDo = this.todolista.length;
        } else if (this.task.isDone) {
          this.tasksLeftToDo = this.todolista.length - 1;
        }
      }
    },
    clickHandler() {
      if (this.field.length < 3) {
        this.error = true;
        this.field = "";
      } else {
        this.error = false;
        this.addThing(this.field);
        this.field = "";
      }
      this.tasksLeft();
    },
    addThing(task) {
      const newThing = {
        id: new Date().toISOString(),
        name: task,
        isDone: false,
      };
      return this.todolista.push(newThing);
    },
    /*   checked(id) {
      this.thing = this.todolista.filter((thing) => thing.id === id);
      for (this.thing in this.todolista) {
        if (this.thing.isDone) {
          this.tasksLeftToDo = this.todolista.length;

          console.log("true to false");
        } else if (!this.thing.isDone) {
          this.tasksLeftToDo = this.todolista.length - 1;

          console.log("false to true");
        }
      }
    }, */
    removeElement(id) {
      this.todolista = this.todolista.filter((thing) => thing.id !== id);
      this.tasksLeft();
      if (this.todolista.length < 1) {
        this.tasksLeftToDo = 0;
      }
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
