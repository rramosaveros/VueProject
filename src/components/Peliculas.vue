<template>
  <div class="general">
    <div class="center">
      <section id="content">
        <h2 class="subheader">Películas</h2>

        <div class="mis-datos" v-if="misDatos">
          <!-- {{misDatos}} forma uno sin imprimir las etiquetas html  -->
          <p v-html="misDatos"></p>
          <br/>
          {{web | mayusculas | concatenaYear('ESTE ES EL MEJOR AÑO') }}
        </div>

        <div class="favorita" v-if="favorita">
          La película favorita es:
          <h3> {{favorita.title}}</h3>
        </div>

        <!--Listado articulos-->
        <div id="articles">
          <div v-for="pelicula in peliculasMayuscula" v-bind:key="pelicula.title">
            <Pelicula 
              :pelicula="pelicula"
              v-on:favorita="haLlegadoPeliculaFavorita" 
            ></Pelicula>
          </div>
        </div>
      </section>
      <Sidebar></Sidebar>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import Pelicula from "./Pelicula.vue";
import Sidebar from './Sidebar.vue';
export default {
  name: "Peliculas",
  components: {
    Pelicula,
    Sidebar
  },
  filters: {
    mayusculas(value){
      return value.toUpperCase(); 
    },
    concatenaYear(value, message){
      var date = new Date(); 
      return value + ' ' + date.getFullYear() + ' ' + message; 
    }

  },
  computed:{
    peliculasMayuscula(){
      var peliculasMod = this.peliculas; 
      for(var i=0; i < this.peliculas.length; i++){
        peliculasMod[i].title = peliculasMod[i].title.toUpperCase();
      }

      return peliculasMod;
    }, 
    misDatos(){
      return this.nombre + ' ' + this.apellidos + '<br/>' + 'Sitio web: <strong>' + this.web + '</strong>'; 
    }
  },
  data() {
    return {
      nombre: 'Lenin',
      apellidos: 'Ramos AVeros',
      web: 'lend.com',
      favorita: null, 
      peliculas: [
        {
          title: "Batman vs Superman",
          year: 2017,
          image:
            "https://occ-0-92-1722.1.nflxso.net/dnm/api/v6/E8vDc_W8CLv7-yMQu8KMEC7Rrr8/AAAABVixGzDct56-tsHGWLZwtml5CejHjH2jjmxSag8NKtgyx7MNfqzhcC5192uzJoo-dpVg0SvdMiLqD37Sx4-MPCRgK0od.jpg?r=2a9",
        },
        {
          title: "Gran Torino",
          year: 2015,
          image:
            "https://carburando.com/sites/default/files/ford_gran_torino.jpg",
        },
        {
          title: "El señor de los anillos",
          year: 2003,
          image:
            "https://upload.wikimedia.org/wikipedia/commons/7/7d/El_Se%C3%B1or_de_los_Anillos_lectura.jpg",
        },
        {
          title: "El señor de los anillos 2",
          year: 2003,
          image:
            "https://upload.wikimedia.org/wikipedia/commons/7/7d/El_Se%C3%B1or_de_los_Anillos_lectura.jpg",
        },
      ],
    };
  },
  methods: {
    haLlegadoPeliculaFavorita(favorita){
      this.favorita = favorita; 
    }
  }
};
</script>