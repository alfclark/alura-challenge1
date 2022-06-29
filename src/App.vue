<template>
  <EncryptionView />
</template>

<script>
import EncryptionView from "./components/EncryptionView.vue";

export default {
  name: "App",
  components: {
    EncryptionView,
  },
};
</script>

<style>
:root {
  --lightBlue: #f3f5fc;
  --mediumBlue: #d8dfe8;
  --darkBlue: #0a3871;
  --lightGrey: #d8dfe8;
  --grey: #495057;
  --darkGrey: #343a40;
  --red: rgb(182, 65, 65);
}
*,
html {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  background-color: var(--lightBlue);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
</style>
