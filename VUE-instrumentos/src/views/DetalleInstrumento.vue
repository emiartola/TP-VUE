<template>
  <div class="container-fluid d-flex container border">
    <div class="row">
      <div class="col-lg-8">
        <b-img :src="'../assets/images/' + instrumentoEncontrado.imagen" style="max-width:50%, max-height= 50%"></b-img>
        <div>
          <p> Descripción : </p>
          <p>{{ instrumentoEncontrado?.descripcion }}</p>
        </div>
      </div>

      <div class="col-lg-4 mt-3" >
        <p>{{ instrumentoEncontrado?.cantidadVendida }} vendidos </p>
        <h2><b>{{ instrumentoEncontrado?.instrumento }}</b></h2>
        <h5>Marca : {{ instrumentoEncontrado?.marca }}</h5>
        <h5>Modelo : {{ instrumentoEncontrado?.modelo }}</h5>
        <h2><b> ${{ instrumentoEncontrado?.precio }}</b></h2>
        Costo Envío:
        <span v-if="instrumentoEncontrado.costoEnvio == 'G'" style="color:green; font-weight: bold;">
          Gratis
        </span>
        <span v-else style="color: orange">
          $ {{ instrumentoEncontrado.costoEnvio }}
        </span>
      </div>
      <b-button variant="primary" class="btn btn-primary" href="/productos"> Volver </b-button>
    </div>
  </div>
</template>

<script lang="ts">
export default {
  name: "DetalleInstrumento",
  components: {},
  mounted() {
    this.getInstrumentoPorId();
  },
  data() {
    return {
      instrumentoEncontrado: [],
    };
  },
  methods: {
    async getInstrumentoPorId() {
      const parametroId = this.$route.params.id;
      const res = await fetch("/instrumentos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.instrumentoEncontrado = await resJson.instrumentos.find(
        (instrumento) => instrumento.id === parametroId
      );
      console.log(this.instrumentoEncontrado);
    },
  },
};
</script>