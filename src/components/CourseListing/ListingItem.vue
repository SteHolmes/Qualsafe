<template>
    <div class="ListingItem">
      <div class="ListingItem-overview">
        <h2 class="ListingItem-heading">Course ID: {{ item.id }}</h2>
        <dl class="ListingItem-details">
          <dt>Start date:</dt>
          <dd>{{ item.start }}</dd>
          <dt>End date:</dt>
          <dd>{{ item.end }}</dd>
          <dt>Qualification:</dt>
          <dd>{{ item.qualification }}</dd>
        </dl>    
      </div>
      <div class="ListingItem-furtherInfo">
        <accordion 
          heading="View enrolled students"
          :items="item.students"
        />
      </div>
    </div>
</template>

<script>
import Accordion from "../Accordion/Accordion.vue";

export default {
  name: "listing-item",
  components: {
    accordion: Accordion,
  },
  data() {
    return {};
  },
  props: {
    item: null,
  },
};
</script>

<style lang="scss">
.ListingItem {
  width: 100%;
  background-color: #ffffff;
  padding: 1.5rem 2rem 1rem 2rem;
  text-align: left;
  border-radius: 0.5rem;
  margin-bottom: 2rem;
  box-sizing: border-box;
  box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.1);

  &-overview {
    width: 100%;
  }

  &-heading {
    width: 100%;
    color: #114c98;
    margin-top: 0;
    padding-bottom: 1rem;
    border-bottom: 1px solid #e5e5e5;
  }

  &-details {
    display: grid;
    grid-template-columns: 25% auto;
    background-color: #ecf7ee;
    padding: 1rem;
    border-radius: 0.5rem;

    dt,
    dd {
      display: inline-block;
    }

    dt {
      font-weight: bold;
    }

    dd:not(:last-child) {
      margin-bottom: 1rem;
    }
  }

  &-status {
    width: 20%;
  }
}
</style>