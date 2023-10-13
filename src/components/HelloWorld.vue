<template>
  <div>
    <h1>{{ titulo }}</h1>
    <label for="pais">País:</label>
    <select id="pais" v-model="paisSeleccionado" @change="listCities">
      <option value="todos">Selecciona un país</option>
      <!-- <option value="todos">Mostrar todos los países</option> -->

    </select>

    <div v-if="paisSeleccionado === 'todos'">
      <h2>Lista de todos los países:</h2>
      <ul>
        <li v-for="country in countries" :key="country.id">{{ country.nombre }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
//axios.defaults.baseURL = 'http://localhost:9999/api/v1/country';

export default {
  data() {
    return {
      titulo: 'Selección de ciudades',
      paisSeleccionado: '',
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
            console.error('Error al obtener la lista de tareas:', error);
          });
    },  
  },
};
</script>
