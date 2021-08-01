<template>
  <div class="general">
    <Slider
      texto="Página 1 de pruebas"
    ></Slider>
    <div class="center">
      <section id="content">
        <h2 class="subheader">Página</h2>
        <h3>{{ id_desde_url }}</h3>
        <button @click="actualizarNombre()">Actualizar Nombre</button>
        <button @click="redirigirBlog()">Redirigir al Blog</button>
        <!-- <button v-on="actualizarNombre()">Actualizar Nombre</button> -->
        <h4>{{ nombre }}</h4>
      </section>
      <Sidebar></Sidebar>
      <div class="clearfix"></div>
    </div>
  </div>
</template>

<script>
import Slider from './Slider.vue';
import Sidebar from './Sidebar.vue';
export default {
  name: "Pagina",
  components: {
    Slider, 
    Sidebar
  },
  created() {
    console.log("Componente creado");
  },
  mounted() {
    // ciclo de vida, lo primero que se ejecuta
    this.id_desde_url = this.$route.params.id;
    console.log("Componente montado");
  },
  updated() {
    console.log("Componente actualizado");
  },
  destroyed() {
    console.log("Componente eliminado");
  },
  data() {
    return {
      id_desde_url: null,
      nombre: "Lenin Ramos",
    };
  },
  methods: {
    actualizarNombre() {
      this.nombre = "LENIN RAMOS";
      console.log(this.nombre);
    },
    redirigirBlog() {
      this.$router.push("/blog");
      // this.$router.push('/blog/dfdsfsfds');
      // this.$router.push({name:'pagina', params: {id: 'Redirección'}});
    },
  },
};
</script>