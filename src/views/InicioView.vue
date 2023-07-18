<template>
  <div>
    <h1>Bienvenido al Inicio</h1>
    <div v-for="misa in misas" :key="misa.id" >
      <b-card
        :title="(misa.tipo)"
        img-src="https://picsum.photos/600/300/?image=25"
        img-alt="Image"
        img-top
        tag="article"
        style="max-width: 20rem"
        class="mb-2"
      >
        <b-card-text>
          {{ misa.fecha }}
        </b-card-text>

        <b-button href="#" @click="regIntencion()" variant="primary">Registrar intencion</b-button>
      </b-card>
    </div>
  </div>
</template>
<script>
export default {
  name: "InicioView",
  data() {
    return {
      misa: {
        id: 0,
        tipo: "",
        fecha: "",
      },
      misas: [],
    };
  },
  methods: {
    regIntencion(){
      this.$router.push('/reginten');
    },

    async listarMisas() {
      await this.axios.get("http://localhost:5000/misa/").then((r) => {
        console.log(r.data.data);
        this.misas = r.data.data;
      });
    },
  },
  mounted() {
    this.listarMisas();
  }
};
</script>
