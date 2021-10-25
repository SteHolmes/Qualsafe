<template>
  <div class="CourseListing">
    <h1 class="CourseListing-heading">
      <svg aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="feather feather-alert-triangle" style="
        width: 2.5rem;
        height: 2.5rem;
        margin-right: 1.5rem;"><path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"></path><line x1="12" y1="9" x2="12" y2="13"></line><line x1="12" y1="17" x2="12.01" y2="17"></line></svg>
        <span>Unpaid Courses</span>
    </h1>
    <div class="CourseListing-container">
      <ul class="CourseListing-list" v-if="courses && courses.length">
        <li v-for="(course, index) in courses" :key="`course-${course.id}`">
          <listing-item
            :item="course"
            :status="statuses[index]" />
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
      statuses: ['Pending', 'Approved', 'Cancelled', 'Approved', 'Pending', 'Pending']
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
    display: flex;
    align-items: center;
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
