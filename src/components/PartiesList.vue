<template>
  <div>
    <party v-on:delete-party="deleteParty"
     v-for="party in parties"
     :key="party.id" :party.sync="party"></party>
  </div>
</template>

<script type = "text/javascript" >
import swal from 'sweetalert';
import Party from './Party';

export default {
  props: ['parties', 'categories'],
  components: {
    Party,
  },
  methods: {
    deleteParty(party) {
      swal(
        {
          title: 'Are you sure?',
          text: 'This party will be permanently deleted!',
          icon: 'warning',
          buttons: true,
          dangerMode: true,
        })
        .then((willDelete) => {
          if (willDelete) {
            const partyIndex = this.parties.indexOf(party);
            this.parties.splice(partyIndex, 1);
            swal('Deleted!', 'Your party has been deleted.', 'success');
          } else {
            swal('Your imaginary file is safe!');
          }
        });
    },
  },
};
</script>

<style scoped>
  p.tasks {
    text-align: center;
  }
</style>
