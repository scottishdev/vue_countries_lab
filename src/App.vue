<template>
  <div id="app">
    <h2>Global population: </h2>

    <label for="country_select">Select a Country:</label>
    <select id="country_select" v-model="selectedCountry">
      <option disabled value="">Select a country</option>
      <option v-for="country in countries" :value="country">{{country.name}}</option>
    </select>

  <!-- Country detail goes here -->
  <h3>Total Population: {{totalPopulation}}</h3>
  <button>Add Country</button>
  <ul>
    <div class="country" v-for="country in countries">
    <li>{{country.name}}</li>
    <img :src="country.flag" width="100" height="70">
    </div>
  </ul>


    <!-- Favourite Countries goes here -->
</div>

</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      countries: [],
      selectedCountry: null,
      favouriteCountries: []
    }
  },
    computed: {
      totalPopulation: function(){
        return this.countries.reduce((accumulator, country) => {
          return accumulator + country.population;
        }, 0);
      }
    },
    mounted(){
      this.getCountries();
    },
    methods: {
      getCountries: function(){
        fetch("https://restcountries.eu/rest/v2/all")
        .then(response => response.json())
        .then(data => this.countries = data);
      }
    }
}
</script>

<style>
.small-flag {
  height: 20px
}



</style>
