<template>
  <div>
    <li :style="taskDoneBackground">
      <input type="checkbox" class="checkbox-round check" @click="toggleTask" />
      <span :style="taskDoneText">{{ element }}</span>

      <button @click="$emit('remove-element', id)" class="remove">x</button>
    </li>
  </div>
</template>

<script>
export default {
  props: {
    element: {
      type: String,
      requried: true,
    },
    id: {
      type: String,
      requried: true,
    },
    taskIsDone: {
      type: Boolean,
      requried: true,
    },
  },
  emits: ["remove-element", "checked-tasks"],
  computed: {
    taskDoneBackground() {
      if (this.isDone) {
        return "background-color: #faffd0; ";
      } else {
        return "background-color: #c4eab6;";
      }
    },
    taskDoneText() {
      if (this.isDone) {
        return "text-decoration: line-through;";
      } else {
        return "text-decoration: none;";
      }
    },
  },
  data() {
    return {
      isDone: false,
    };
  },
  methods: {
    toggleTask() {
      this.isDone = !this.isDone;
      this.$emit("checked-tasks", this.id);
    },
  },
};
</script>

<style scoped>
li {
  background-color: #c4eab6;
  padding: 15px;
  padding-left: 5px;

  margin-bottom: 4px;
  align-content: center;
  display: flex;

  align-self: center;
  position: relative;
}

.checkbox-round {
  width: 20px;
  height: 20px;
  background-color: white;
  border-radius: 50%;
  vertical-align: middle;
  border: 2px solid #ddd;
  -webkit-appearance: none;
  outline: none;
  cursor: pointer;
}

.checkbox-round:checked {
  background-color: #5ca15c;
}
.check {
  align-self: center;
}
button {
  border-radius: 20%;
  width: 30px;
  height: 25px;
  border: none;
  background-color: #5ca15c;
  color: white;
  vertical-align: middle;
  position: absolute;
  right: 10px;
  cursor: pointer;
  outline: none;
}
button:hover,
button:active {
  background-color: #e96c6c;
  border-color: #ec3169;
  border-radius: 20%;
  cursor: pointer;
  outline: none;
}
</style>
