<template>
  <article class="Accordion" :class="accordionClasses">
      <div class="Accordion-header" @click="toggleAccordion">
          {{ heading }}    
      </div>
      <div class="Accordion-body">
          <ul class="Accordion-list">
            <li v-for="item in items" :key="`student-${item.id}`" class="Accordion-listItem">
              <span><strong>ID:</strong> {{ item.id }}</span>
              <span><strong>Name:</strong> {{ item.name }}</span>
            </li>
          </ul> 
      </div>
  </article>
</template>

<script>
export default {
  name: "accordion",
  data() {
    return {
      isOpen: false,
    };
  },
  props: {
    heading: String,
    items: null,
  },
  computed: {
    accordionClasses: function () {
      return {
        "is-closed": !this.isOpen,
        "is-open": this.isOpen,
      };
    },
  },
  methods: {
    toggleAccordion() {
      this.isOpen = !this.isOpen;
    },
  },
};
</script>

<style scoped lang="scss">
.Accordion {
  &-header {
    font-weight: bold;
    cursor: pointer;
    color: #024699;
    transition: color 0.3s ease-in;

    &:after {
      .Accordion.is-closed & {
        content: "\002B";
      }

      .Accordion.is-open & {
        content: "\2212";
      }
    }

    &:hover {
      color: lighten(#024699, 15%);
    }
  }

  &-body {
    padding-top: 0.5rem;
    height: 0px;
    opacity: 0;
    visibility: hidden;
    transition: height 0.3s ease-in opacity 0.5s ease-in;

    .Accordion.is-open & {
      height: 100%;
      opacity: 1;
      visibility: visible;
    }
  }

  &-list {
    list-style-type: none;
    padding: 0;
    opacity: 0;
    visibility: hidden;
    transform: translateY(-10px);
    transition: all 0.3s ease-in;

    .Accordion.is-open & {
      height: 100%;
      opacity: 1;
      visibility: visible;
      transform: translateY(0);
    }
  }

  &-listItem {
    padding: 0.5rem 0rem;
    border-bottom: 1px solid #e5e5e5;

    span + span {
      margin-left: 1rem;
    }
  }
}
</style>