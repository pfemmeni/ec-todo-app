<template>
  <div class="positioning" v-if="isOpen">
    <div>
      This website uses cookies to ensure you get the best experience on our
      website.
    </div>
    <div>
      <button @click="acceptCookies">Accept</button>
      <button @click="denyCookies">Deny</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: true,
    };
  },
  methods: {
    getCookies() {
      return localStorage.getItem("Accepted");
    },
    acceptCookies() {
      this.isOpen = false;
      localStorage.setItem("Accepted", "true");
    },
    denyCookies() {
      this.isOpen = false;
      localStorage.setItem("Accepted", "false");
    },
  },
  created() {
    if (this.getCookies() === "true") {
      this.isOpen = false;
    }
  },
};
</script>

<style scoped>
.positioning {
  position: fixed, top;
  background-color: #b8e5b6;
  margin: none;
  padding: 15px;
  color: darkgreen;
}
button {
  margin-top: 8px;
  margin-right: 10px;
  background-color: #5ca15c;
  color: white;
  outline: none;
  border: none;
  padding: 5px;
}
</style>
