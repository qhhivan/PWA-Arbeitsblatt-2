<template>
  <div
    id="app"
    class="
      container
      d-flex
      flex-column
      justify-content-center
      align-items-center
      mt-5
    "
  >
  <h3>Willkommen bei der Service Worker Untersuchung!</h3>
    <ButtonGet @get="fetchData"></ButtonGet>

    <CardView :employees="employees" @del="delEmployee"></CardView>
  </div>
</template>

<script>
import ButtonGet from '@/components/ButtonGet.vue';
import CardView from '@/components/CardView.vue';

// Axios
import axios from 'axios';

export default {
  name: 'app',
  components: {
    ButtonGet,
    CardView,
  },
  data() {
    return {
      serverAddress: process.env.VUE_APP_SERVER,
      employees: [],
    };
  },
  methods: {
    async fetchData() {
      console.log('fetchData called');
      // axios Call Daten vom Server Holen und in employees hinzufügen
      try {
        const { data } = await axios.get('http://localhost:3000/employees');
        this.employees = data;
        // console.log(this.employees);
        console.log('OK');
      } catch (error) {
        console.log(error.message);
      }
    },

    delEmployee(e) {
      console.log('delEmployee called');
      // axios call Delete
      try {
        // console.log(e.id);
        axios.delete(`http://localhost:3000/employees/${e.id}`);
        this.fetchData();
        console.log('Gelöscht');
      } catch (error) {
        console.log(error.message);
      }
    },
  },
};
</script>

<style></style>
