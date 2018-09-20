<template>
  <div class='ui basic content center aligned segment'>
    <button class='ui basic button icon' v-on:click="openForm" v-show="!isCreating">
      <i class='plus icon'></i>
    </button>
    <div class='ui centered card' v-show="isCreating">
      <div class='content left aligned'>
        <div class='ui form'>
          <div class='field'>
            <label>Название</label>
            <input v-model="nameText" type='text'>
          </div>
          <div class='field'>
            <label>Описание</label>
            <input v-model="descriptionText" type='text'>
          </div>
          <div class="field">
            <div class="ui checkbox">
              <input type="checkbox"  v-model="isFreeEntryCheckbox">
              <label>Свободный вход</label>
            </div>
          </div>
          <div class="two fields">
            <div class='field'>
              <label>Дата</label>
              <datepicker v-model="dateField" format="yyyy-MM-d"></datepicker>
            </div>
            <div class='field'>
              <label>Время</label>
              <input type="time" class="form-control" placeholder="Date" v-model="timeField">
            </div>
          </div>
          <div class='field'>
            <label>Цена</label>
            <input type='number' v-model="priceField" >
          </div>
          <div class='field'>
            <label>Адрес</label>
            <input type='text' v-model="addressField" >
          </div>
           <div class="field">
          <label>Категория</label>
            <select class="ui fluid dropdown"  v-model="categoryField">
              <option value="">Категория:</option>
              <option v-for="category in categories" category.sync="category"
              :key="category.id"> {{category.name}} </option>
            </select>
          </div>
          <div class='ui two button attached buttons'>
            <button class='ui basic blue button' v-on:click="sendForm()">
              Create
            </button>
            <button class='ui basic red button' v-on:click="closeForm">
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker';
import moment from 'moment';

export default {
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
      nameText: '',
      descriptionText: '',
      isFreeEntryCheckbox: false,
      dateField: '',
      timeField: '',
      priceField: 0,
      addressField: '',
      categoryField: '',
      isCreating: false,
    };
  },
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.nameText.length > 0 && this.descriptionText.length > 0) {
        const name = this.nameText;
        const description = this.descriptionText;
        const isFreeEntry = this.isFreeEntryCheckbox;
        const date = moment(this.dateField).format('YYYY-MM-DD');
        const time = this.timeField;
        const price = this.priceField;
        const address = this.addressField;
        const category = this.categoryField;
        this.$emit('create-party', {
          name,
          description,
          isFreeEntry,
          date,
          time,
          price,
          address,
          category,
        });
        this.nameText = '';
        this.descriptionText = '';
        this.isFreeEntryCheckbox = false;
        this.dateField = '';
        this.timeField = '';
        this.priceField = 0;
        this.addressField = '';
        this.categoryField = '';
        this.isCreating = false;
      }
    },
  },
};
</script>
