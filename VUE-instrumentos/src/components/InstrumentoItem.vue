<template>
<NavBar></NavBar>
  <div className="col-mb-3 ml-3">
    <div className="card mb-3" style="max-width: 1000px">
      <div className="row no-gutters">
        <div className="col-md-3">
          <img :src="urlImage" className="card-img" alt="item" />
        </div>
        <div className="col-md-8">
          <div className="card-body">
            <h3 className="card-title">{{ instrumentoParam.nombre }}</h3>
            <br>
            <h2> $ {{ instrumentoParam.precio }} </h2>

            {{ instrumentoParam.costoEnvio === "G" }} ? (
            <h5 style= "color: green">
              <img :src="images/camion.png" alt="envioIcon" />
              Envío gratis a todo el país
            </h5>
            ) : (
            <h5 style= "color:orange" >
              Costo del envío al interior de Argentina: {{instrumentoParam.costoEnvio}}
            </h5>
            )}
            <p className="card-text">{{instrumentoParam.cantidadVendida}} vendidos</p>
          </div>
        </div>
      </div>
      <div>
        <a :href="'/detalle/' + instrumentoParam.id" style="width: 100%;" class="btn btn-primary"> Detalle </a>
      </div>
    </div>
  </div>

</template>

<script>
import NavBar from './NavBar.vue';
export default {
    data() {
        return {
            urlImage: String
        };
    },
    props: ["instrumentoParam"],
    mounted() {
        if (String(this.instrumentoParam.imagenPath).indexOf("http") >= 0) {
            this.urlImage = this.instrumentoParam.imagenPath;
        }
        else {
            this.urlImage = "/assets/images/" + this.instrumentoParam.imagenPath;
        }
    },
    components: { NavBar }
};
</script>
