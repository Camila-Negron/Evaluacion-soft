<template>
  <div>
    <h1>{{ titulo }}</h1>
    <label for="pais">País:</label>
    <select id="pais" v-model="paisSeleccionado" @change="listCities">
      <option value="todos">Selecciona un país</option>
      <option v-for="country in countries" :key="country.id" :value="country.nombre">{{ country.nombre }}</option>
    </select>

  </div>
</template>


<script>
import axios from 'axios';
/* axios.defaults.baseURL = 'http://localhost:9999/api/v1'; */

export default {
  data() {
    return {
      countries: []
    };
  },
  mounted() {
    this.listCountries(); 
  },
  methods: {
    listCountries() {
      axios.get('http://localhost:9999/api/v1/country') 
        .then(response => {
          this.countries = response.data;
        })
          .catch(error => {
            console.error('Error al obtener la lista de paises:', error);
          });
    },  
  },
};
</script>
