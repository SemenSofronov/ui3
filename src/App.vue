
<template>
  <div id="app">
    <h1 class="ui dividing centered header">Vue.js Party App</h1>
    <div class="ui two item menu">
      <a class="item active" v-on:click="showForm">Вечеринки</a>
      <a class="item" v-on:click="hideForm">Категории</a>
    </div>
    <div class='ui one column centered grid'>
      <div class='column'>
        <parties-list v-bind:parties="parties" v-show="isSelectedParties"></parties-list>
        <create-party v-on:create-party="createParty" v-show="isSelectedParties"></create-party>
        <category v-show="!isSelectedParties"></category>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert';
import $ from 'jquery';
import PartiesList from './components/PartiesList';
import CreateParty from './components/CreateParty';
import Category from './components/Category';

export default {
  name: 'app',
  components: {
    PartiesList,
    CreateParty,
    Category,
  },
  data() {
    return {
      isSelectedParties: true,
      categories: [{
        name: 'Концерт',
      }, {
        name: 'Квартирник',
      }, {
        name: 'Клубная вечеринка',
      }],
      parties: null,
    };
  },
  methods: {
    createParty(newParty) {
      this.parties.push(newParty);
      swal('Success!', 'Party created!', 'success');
    },
    showForm() {
      this.isSelectedParties = true;
    },
    hideForm() {
      this.isSelectedParties = false;
    },
  },
  mounted() {
    $.getJSON('/static/data/data.json', (data) => {
      this.parties = data;
    });
  },
  created() {
    this.$emit('get-categories', this.categories);
  },
};
</script>

<style>
 @media screen and (min-device-width: 1200px) and (max-device-width: 1600px) and (-webkit-min-device-pixel-ratio: 1) {
    /* .column{
        /* widows:; */
  /* } */
 }
/* landscape */
 @media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: landscape) {
 }
 /* portrait */
@media only screen and (min-device-width: 768px) and (max-device-width: 1024px) and (orientation: portrait) {
}
/* landscape */
@media only screen and (min-device-width: 320px) and (max-device-width: 736px) and (orientation: landscape) {
}
/* portrait */
@media only screen and (min-device-width: 320px) and (max-device-width: 736px) and (orientation: portrait) {
}
</style>
