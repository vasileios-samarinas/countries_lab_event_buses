<template>
  <div id="app">
    <h1>Countries<span>dot</span></h1>
    <div class="box-container">
      <countries-list :countries='countries'></countries-list>
      <country-detail :country='selectedCountry'></country-detail>
    </div>
  </div>
</template>

<script>
import CountriesList from './components/CountriesList.vue';
import CountryDetail from './components/CountryDetail.vue';
import {eventBus} from './main.js';

export default {
  name: 'App',
  data(){
    return {
      countries: [],
      selectedCountry: null
    };
  },
  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail

  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected',(country)=>{
      this.selectedCountry=country;
    })
  }
}
</script>

<style>

#app{
  text-align: center;
}
.box-container {
  display: flex;
  justify-content: space-between;
  width: 40%;
}

h1 {
  font-size: 120px;
}

h1 span {
  font-size: 40px;
  color: #89B802;
}
</style>
