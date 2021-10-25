<template>
    <div class="ListingItem">
      <div class="ListingItem-overview">
        <h2 class="ListingItem-heading">Course ID: {{ item.id }}</h2>
        <div class="ListingItem-body">
          <dl class="ListingItem-details">
            <dt>Start date:</dt>
            <dd>{{ item.start }}</dd>
            <dt>End date:</dt>
            <dd>{{ item.end }}</dd>
            <dt>Qualification:</dt>
            <dd>{{ item.qualification }}</dd>
          </dl>
          <div class="ListingItem-status">
            <h3 class="ListingItem-statusHeading">Status</h3>        
            <!--- Example using a Vue transition tag
            <transition name="bounce">
              <span class="ListingItem-statusText">{{ currentStatus }}</span>
            </transition> -->
            <div v-if="currentStatus === 'Approved'" class="ListingItem-icon">
              <svg version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 130.2 130.2">
                <circle class="path circle" fill="none" stroke="#73AF55" stroke-width="6" stroke-miterlimit="10" cx="65.1" cy="65.1" r="62.1"/>
                <polyline class="path check" fill="none" stroke="#73AF55" stroke-width="6" stroke-linecap="round" stroke-miterlimit="10" points="100.2,40.2 51.5,88.8 29.8,67.5 "/>
              </svg>
            </div>
            <div v-else-if="currentStatus === 'Cancelled'" class="ListingItem-icon">
              <svg version="1.1" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 130.2 130.2">
                <circle class="path circle" fill="none" stroke="#D06079" stroke-width="6" stroke-miterlimit="10" cx="65.1" cy="65.1" r="62.1"/>
                <line class="path line" fill="none" stroke="#D06079" stroke-width="6" stroke-linecap="round" stroke-miterlimit="10" x1="34.4" y1="37.9" x2="95.8" y2="92.3"/>
                <line class="path line" fill="none" stroke="#D06079" stroke-width="6" stroke-linecap="round" stroke-miterlimit="10" x1="95.8" y1="38" x2="34.4" y2="92.2"/>
              </svg>
            </div>
            <div v-else class="ListingItem-icon ListingItem-icon--pending">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ListingItem-icon--inline feather feather-clock"><circle cx="12" cy="12" r="10"></circle><polyline points="12 6 12 12 16 14"></polyline></svg>
              <span>Pending</span>
            </div>
            <div class="ListingItem-buttonContainer">
              <button v-if="currentStatus !== 'Approved'" @click="currentStatus = 'Approved'" class="ListingItem-button ListingItem-button--approve">Approve</button>
              <button v-if="currentStatus !== 'Cancelled'" @click="currentStatus = 'Cancelled'" class="ListingItem-button ListingItem-button--cancel">Cancel</button>
            </div>
          </div> 
        </div>  
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
    return {
      show: true,
      currentStatus: this.status,
    };
  },
  props: {
    item: null,
    status: null,
  },
};
</script>

<style lang="scss">
.ListingItem {
  width: 100%;
  background-color: #fff;
  padding: 1.25rem;
  text-align: left;
  border-radius: 0.5rem;
  margin-bottom: 2rem;
  box-sizing: border-box;
  box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.1);

  @media only screen and (min-width: 768px) {
    padding: 1.5rem 2rem 1rem 2rem;
  }

  &-overview {
    width: 100%;
  }

  &-heading {
    width: 100%;
    color: #3381a2;
    margin-top: 0;
    padding-bottom: 1rem;
    border-bottom: 1px solid #e5e5e5;
  }

  &-body {
    @media only screen and (min-width: 768px) {
      display: grid;
      grid-template-columns: 75% auto;
    }
  }

  &-details {
    display: grid;
    grid-template-columns: auto auto;
    background-color: #cde9f4;
    padding: 1rem;
    margin: 0;
    border-radius: 0.5rem 0.5rem 0 0;

    @media only screen and (min-width: 768px) {
      grid-template-columns: 25% auto;
      border-radius: 0.5rem 0 0 0.5rem;
    }

    dt,
    dd {
      display: inline-block;
      margin: 0;
    }

    dt {
      font-weight: bold;
    }

    dd:not(:last-child) {
      margin-bottom: 1rem;
    }
  }

  &-status {
    display: grid;
    grid-template-rows: 20% 55% auto;
    width: 100%;
    min-height: 130px;
    padding-top: 1rem;
    text-align: center;
    border: 1px solid #e5e5e5;
    border-radius: 0 0 0.5rem 0.5rem;
    box-sizing: border-box;
    overflow: hidden;

    @media only screen and (min-width: 768px) {
      border-radius: 0 0.5rem 0.5rem 0;
    }

    &Heading {
      color: #3381a2;
    }

    &Heading,
    &Text {
      margin: 0;
    }
  }

  &-furtherInfo {
    margin-top: 1.5rem;
  }

  &-icon {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0.5rem;

    &--pending {
      color: #FF9933;
      font-weight: bold;

      svg {
        width: 1.5rem !important;
        margin-right: 0.375rem;
      }
    }

    svg {
      width: 50px;
      max-height: 100%;
      display: block;
    } 
  }

  &-buttonContainer {
    display: flex;
  }

  &-button {
    outline: none;
    box-shadow: none;
    border: none;
    color: #fff;
    font-weight: bold;
    background: #3381a2;
    cursor: pointer;
    text-transform: uppercase;
    transition: background 0.3s ease-in;
    flex-basis: 100%;

    &--approve {
      background: #4190af;
      &:hover {
        background: darken(#3381a2, 15%);
      }
    }

    &--cancel {
      background: #b23c27;
      &:hover {
        background: darken(#b23c27, 15%);
      }
    }
  }
}

/* Vue transition tag example
.bounce-enter-active {
  animation: bounce-in .5s;
}
.bounce-leave-active {
  animation: bounce-in .5s reverse;
}*/

/*@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}*/

.path {
  stroke-dasharray: 1000;
  stroke-dashoffset: 0;

  &.circle {
    -webkit-animation: dash .9s ease-in-out;
    animation: dash .9s ease-in-out;
  }

  &.line {
    stroke-dashoffset: 1000;
    -webkit-animation: dash .9s .35s ease-in-out forwards;
    animation: dash .9s .35s ease-in-out forwards;
  }

  &.check {
    stroke-dashoffset: -100;
    -webkit-animation: dash-check .9s .35s ease-in-out forwards;
    animation: dash-check .9s .35s ease-in-out forwards;
  }
}

@-webkit-keyframes dash {
  0% {
    stroke-dashoffset: 1000;
  }
  100% {
    stroke-dashoffset: 0;
  }
}

@keyframes dash {
  0% {
    stroke-dashoffset: 1000;
  }
  100% {
    stroke-dashoffset: 0;
  }
}

@-webkit-keyframes dash-check {
  0% {
    stroke-dashoffset: -100;
  }
  100% {
    stroke-dashoffset: 900;
  }
}

@keyframes dash-check {
  0% {
    stroke-dashoffset: -100;
  }
  100% {
    stroke-dashoffset: 900;
  }
}


</style>