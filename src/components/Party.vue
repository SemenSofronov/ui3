<template>
  <div class='ui centered card'>
    <div class="content" v-show="!isEditing">
      <span class='right floated edit icon' v-on:click="showForm">
            <i class='edit icon'></i>
          </span>
          <span class='right floated trash icon' v-on:click="deleteParty(party)">
            <i class='trash icon'></i>
          </span>
      <div class='header'>
          {{ party.name }}
      </div>
      <div class='meta'>
          <span class='calendar icon' v-if="party.date">
            <i class='calendar icon'></i>
            {{ party.date }}
          </span>
          <span class='time icon' v-if="party.time">
            <i class='time icon'></i>
            {{ party.time }}
          </span>
          <span class='right floated ruble sign icon' v-if="party.price">
            <i class='ruble sign icon'></i>
            {{ party.price }}
          </span>
      </div>
      <div class="description">
         {{ party.description }}
         <br>
         {{ party.address }}
      </div>
      <div class="ui read-only checkbox">
        <input type="checkbox" tabindex="0" class="hidden" v-model="party.isFreeEntry">
        <label>Свободный вход</label>
      </div>
    </div>
      <div class='extra content'>
        {{party.category}}
      </div>
    <div class="content" v-show="isEditing">
      <div class='ui form'>
        <div class='field'>
          <label>Название</label>
          <input type='text' v-model="party.name" >
        </div>
        <div class='field'>
          <label>Описание</label>
          <input type='text' v-model="party.description" >
        </div>
        <div class="inline field">
          <div class="ui checkbox">
            <input type="checkbox" v-model="party.isFreeEntry">
            <label>Свободный вход</label>
          </div>
        </div>
        <div class="two fields">
          <div class='field'>
            <label>Дата</label>
            <datepicker v-model="party.date" format="yyyy-MM-d"></datepicker>
          </div>
          <div class='field'>
            <label>Время</label>
            <input type="time" class="form-control" placeholder="Date" v-model="party.time">
          </div>
        </div>
        <div class='field'>
          <label>Цена</label>
          <input type='number' v-model="party.price" >
        </div>
        <div class='field'>
          <label>Адрес</label>
          <input type='text' v-model="party.address" >
        </div>
        <div class="field">
          <label>Категория</label>
            <select class="ui fluid dropdown"  v-model="party.category">
              <option value="">Категория</option>
              <option v-for="category in categories" category.sync="category" :key="category.id">
                {{category.name}}
              </option>
            </select>
          </div>
        <div class='ui two button attached buttons'>
          <button class='ui basic blue button' v-on:click="hideForm">
            Close X
          </button>
        </div>
      </div>
    </div>

  </div>
</template>

<script type="text/javascript">
import Datepicker from 'vuejs-datepicker';

export default {
  props: ['party'],
  components: {
    Datepicker,
  },
  data() {
    return {
      categories: [{
        name: 'Концерт',
      }, {
        name: 'Квартирник',
      }, {
        name: 'Клубная вечеринка',
      }],
      isEditing: false,
    };
  },
  methods: {
    deleteParty(party) {
      this.$emit('delete-party', party);
    },
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
  },
  // created() {
  //   this.$on("get-categories", evt => {
  //     this.categories.push(newCategories);
  //   });
  // },
};
</script>
