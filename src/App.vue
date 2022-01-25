<template>
  <CThemeProvider>
    <CReset />
    <div id="app">
      <Main />
    </div>
  </CThemeProvider>
</template>

<script>
import Main from "@/views/Main.vue";
import { CThemeProvider, CReset } from "@chakra-ui/vue";

export default {
  name: "App",
  components: {
    Main,
    CThemeProvider,
    CReset,
  },
};
</script>

<style>
</style>
