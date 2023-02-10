<template>
  <main>
    <form action="">
      <label for="cityAddInput">Lägg till stad</label>
      <input v-model="cityNameInput" type="text" />

      <label for="cityAddInput">Population</label>
      <input v-model="cityPopulation" type="number" />

      <input id="btn" type="button" value="Lägg till" @click="AddCity" />
    </form>
    <div id="cityContainer">
      <div class="city" v-for="city in cities" :key="city.id">
        <h2>{{ city.name }} - {{ city.population }}</h2>
      </div>
    </div>
  </main>
</template>

<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        cities: [],
        cityNameInput: '',
        cityPopulation: 0
      };
    },

    async created() {
      this.fetchAllCities();
    },
    methods: {
      AddCity() {
        const response = axios
          .post('https://avancera.app/cities', {
            name: this.cityNameInput,
            population: this.cityPopulation
          })
          .then((response) => console.log('response', response));

        this.fetchAllCities();
      },
      async fetchAllCities() {
        const reponse = await axios.get('https://avancera.app/cities');
        this.cities = reponse.data;
      }
    }
  };
</script>

<style>
  #cityAddInput {
    display: block;
  }

  #btn {
    width: 200px;
  }
</style>
