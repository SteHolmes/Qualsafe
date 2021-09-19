<template>
  <div class="CourseListing">
    <h1 class="CourseListing-heading">Unpaid Courses</h1>
    <div class="CourseListing-container">
      <ul class="CourseListing-list" v-if="courses && courses.length">
        <li v-for="course in courses" :key="`course-${course.id}`">
          <listing-item
            :item="course" />
        </li>
      </ul>
      <p v-else-if="!courses.length">There are currently no outstanding course payments.</p>
      <div v-if="error" class="CourseListing-errorContainer">
        <p>An error occured. Please try again.</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ListingItem from "./ListingItem.vue";

export default {
  name: "course-listing",
  components: {
    "listing-item": ListingItem,
  },
  data() {
    return {
      data: null,
      courses: [],
      heading: null,
      results: null,
      error: false,
    };
  },
  props: {
    endpointUrl: String,
  },
  mounted() {
    this.fetchData(this.endpointUrl);
  },
  methods: {
    fetchData(url) {
      axios
        .get(url)
        .then((resp) => {
          if (resp.data) {
            this.data = resp.data;
            this.courses = this.data.courses;
          }
        })
        .catch((err) => {
          console.error(`Error : ${err}`);
          this.error = true;
        });
    },
  },
};
</script>

<style scoped lang="scss">
.CourseListing {
  &-heading {
    width: 100%;
    color: #fff;
    border: 2px solid #fff;
    text-align: left;
    margin-bottom: 1.75rem;
    padding: 1rem 2rem;
    box-sizing: border-box;
    border-radius: 0.5rem;
  }

  &-list {
    list-style-type: none;
    padding: 0;
  }

  &-errorContainer {
    padding: 1rem 2rem;
    background-color: #fff;
    color: #eb6448;
    border-radius: 0.75rem;
  }
}
</style>
