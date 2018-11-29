<template>
  <Frame id="mainframe" xmlns="http://schemas.nativescript.org/tns.xsd">

    <template v-if="completedWelcome">
      <start-page></start-page>
    </template>

    <template v-else>
      <welcome-screen></welcome-screen>
    </template>

  </Frame>
</template>

<script>
  import StartPage from "./StartPage";
  import * as applicationSettings from 'tns-core-modules/application-settings';
  import WelcomeScreen from "./WelcomeScreen";

  export default {
    components: {WelcomeScreen, StartPage},
    data() {
      return {

      }
    },
    computed: {
      completedWelcome() {
        return applicationSettings.getBoolean('completed-welcome', false);
      }
    }
  }
</script>

<style scoped>



</style>
