<template>
  <div>
    <div>{{ cookieObject.message }}</div>
    <div>
      <button @click="acceptCookies">
        {{ cookie.Object.acceptButtonText }}
      </button>
      <button @click="denyCookies">{{ cookieObject.denyButtonText }}</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cookieObject: Object,
  },
  data() {
    return {
      isOpen: true,
    };
  },
  methods: {
    getCookies() {
      return localStorage.getItem("Accepted", true);
    },
    acceptCookies() {
      this.isOpen = false;
      localStorage.setItem("Accepted", true);
    },
    denyCookies() {
      this.isOpen = false;
      localStorage.setItem("Accepted", false);
    },
  },
  created() {
    if (this.getCookies() === true) {
      this.isOpen = true;
    }
  },
};
</script>

<style scoped></style>
