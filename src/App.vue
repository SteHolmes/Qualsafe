<template>
  <div id="app" class="Container">
    <course-listing 
    :endpointUrl="webServiceUrl" />
  </div>
</template>

<script>
import CourseListing from "./components/CourseListing/CourseListing.vue";

export default {
  name: "App",
  components: {
    "course-listing": CourseListing,
  },
  data() {
    return {
      webServiceUrl: "https://api.jsonbin.io/b/6147442a9548541c29b4de2e",
    };
  },
};
</script>

<style lang="scss">
body {
  background-image: linear-gradient(
    to left top,
    #ceddf3,
    #c6dbf1,
    #bed8ef,
    #b5d6ec,
    #add4e8
  );
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}

.Container {
  $mobile-padding: 1rem;
  $desktop-padding: 2rem;

  padding-left: $mobile-padding / 2;
  padding-right: $mobile-padding / 2;
  margin: 0 auto;
  width: calc(100% - #{$mobile-padding});

  @media only screen and (min-width: 768px) {
    max-width: calc(768px - #{$mobile-padding});
  }

  @media only screen and (min-width: 992px) {
    padding-left: $desktop-padding / 2;
    padding-right: $desktop-padding / 2;
    width: calc(100% - #{$desktop-padding});
    max-width: calc(1024px - #{$desktop-padding});
  }

  @media only screen and (min-width: 1200px) {
    max-width: calc(1200px - #{$desktop-padding});
  }
}
</style>
