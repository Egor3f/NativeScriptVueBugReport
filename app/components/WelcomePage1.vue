<template>
  <Page xmlns="http://schemas.nativescript.org/tns.xsd" actionBarHidden="true">
    <FlexboxLayout>
      <Image src="~/assets/images/welcome_image.jpg"/>
      <Label :text="welcomeText" textWrap="true"/>
    </FlexboxLayout>
  </Page>
</template>

<script>

  export default {
    name: "WelcomePage1",
    props: {},
    data() {
      return {
        welcomeText: 'Welcome Text'
      }
    },
  }
</script>

<style lang="scss" scoped>

  FlexboxLayout {
    flex-direction: column;
    width: 100%;
    height: 100%;
    padding: 10;

    Image {
      flex-grow: 1;
      width: 80%;
      stretch: aspectFit;
      horizontal-align: center;
    }

    Label {
      flex-grow: 0;
      height: 80;
      width: 100%;
      margin: 10;
      font-size: 16;
      text-align: center;
    }
  }

</style>