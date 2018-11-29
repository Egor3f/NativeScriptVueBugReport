<template>
  <Page @loaded="backButtonSetHandler" @unloaded="backButtonResetHandler" actionBarHidden="true" xmlns="http://schemas.nativescript.org/tns.xsd">

    <FlexboxLayout class="outer">

      <Frame ref="welcomeFrame">
        <welcome-page1></welcome-page1>
      </Frame>

      <StackLayout orientation="horizontal" class="buttons">
        <Button class="back" text="Back" @tap="prevPage" :visibility="currentPageIndex > 0 ? 'visible' : 'hidden'"/>
        <Button class="next" text="Next" @tap="nextPage" v-if="currentPageIndex < totalPages - 1"/>
        <Button class="next" text="Start" @tap="startApp" v-if="currentPageIndex === totalPages - 1"/>
      </StackLayout>

    </FlexboxLayout>

  </Page>
</template>

<script>
  import WelcomePage1 from "./WelcomePage1";
  import StartPage from "./StartPage";
  import * as application from "tns-core-modules/application";

  export default {
    name: "WelcomeScreen",
    components: {WelcomePage1},
    data() {
      return {
        currentPageIndex: 0,
        totalPages: 2,
        pages: [
            WelcomePage1,
            WelcomePage1
        ],
      }
    },
    methods: {
      startApp() {
        // settings.setBoolean('completed-welcome', true);
        this.$navigateTo(StartPage, {
          transition: {
            name: 'fade',
            duration: 300,
            curve: 'linear'
          },
          clearHistory: true,
          frame: 'mainframe'
        });
      },
      nextPage() {
        this.currentPageIndex++;
        this.$navigateTo(this.pages[this.currentPageIndex],
            {
              transition: {
                name: 'slide',
                duration: 300,
                curve: 'easeOut'
              },
              frame: this.$refs.welcomeFrame
            });
      },
      prevPage() {
        this.currentPageIndex--;
        this.$navigateBack({frame: this.$refs.welcomeFrame});
      },
      backButtonSetHandler() {
        application.android.on(application.AndroidApplication.activityBackPressedEvent, this.processBack);
      },
      backButtonResetHandler() {
        application.android.off(application.AndroidApplication.activityBackPressedEvent, this.processBack);
      },
      processBack(args) {
        if(this.currentPageIndex !== 0) args.cancel = true;
      }
    }
  }
</script>

<style lang="scss" scoped>

  .outer {
    width: 100%;
    height: 100%;
    padding: 10 5 10 5;
    flex-direction: column;
    align-items: center;

    Frame {
      width: 100%;
    }

    .buttons {
      width: 100%;
      height: 50;
      flex-shrink: 0;
      margin: 5 5 5 5;
    }

    Button {
      width: 50%;
    }

    Button.back {
      horizontal-align: left;
    }

    Button.next {
      horizontal-align: right;
    }
  }

</style>