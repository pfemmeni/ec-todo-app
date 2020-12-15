<template>
  <div>
    <li :class="{ done: element.isDone }">
      <input
        type="checkbox"
        class="checkbox-round check"
        @click="toggleTask"
        :checked="element.isDone"
      />
      <span :style="taskDoneText">{{ element.name }}</span>

      <button @click="$emit('remove-element', id)" class="remove">x</button>
    </li>
  </div>
</template>

<script>
export default {
  props: {
    element: Object,
  },
  emits: ["remove-element", "checked-tasks"],

  methods: {
    toggleTask() {
      this.$emit("checked-tasks");
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
.done {
  background-color: #faffd0;
  text-decoration: line-through;
}
</style>
