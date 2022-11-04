<template>
  <section class="src-componentes-formulario">
    <div class="jumbotron">
      <h2>Ingresa tus datos</h2>

      <br />

      <vue-form :state="formState" @submit.prevent="enviar()">
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.nombre"
            name="nombre"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            no-espacios
          />

          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="maxlength" class="alert alert-danger mt-1">
              Este campo debe poseer como maximo
              {{ nombreMinLength }} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no permite espacios intermedios
            </div>
          </field-messages>
        </validate>

        <br />

        <validate tag="div">
          <label for="descripcion">Descripcion</label>
          <input
            type="text"
            id="descripcion"
            class="form-control"
            autocomplete="off"
            v-model.trim="formData.descripcion"
            name="descripcion"
            required
            :minlength="descripcionMinLength"
            no-espacios
          />

          <field-messages name="descripcion" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo debe poseer al menos {{ nombreMinLength }} caracteres.
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              Este campo no permite espacios intermedios
            </div>
          </field-messages>
        </validate>

        <br />

        <validate tag="div">
          <label for="importe">Importe</label>
          <input
            type="number"
            id="importe"
            class="form-control"
            autocomplete="off"
            v-model.number="formData.importe"
            name="importe"
            required
            :min="importeMin"
            :max="importeMax"
          />

          <field-messages name="importe" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="min" class="alert alert-danger mt-1">
              El importe no puede ser menor a ${{ importeMin }}
            </div>
            <div slot="max" class="alert alert-danger mt-1">
              El importe no puede ser mayor a ${{ importeMax }}
            </div>
          </field-messages>
        </validate>

        <br />

        <button class="btn btn-success my-3" :disabled="formState.$invalid">
          Enviar
        </button>

        <br />

        <div>
          <p><b>Presupuesto</b></p>
        
          <input
            type="number"
            class="form-control"
            v-model="presupuesto"
            :style="{ color: getColorPresupuesto }"
          />
          
        </div>

        <br />

        <div v-if="datos.length" class="table-responsive">
          <table class="table table-dark">
            <tr>
              <th>Nombre</th>
              <th>Descripcion</th>
              <th>Importe</th>
              <th>Fecha</th>
            </tr>
            <tr v-for="(dato, index) in datos" :key="index">
              <td>{{ dato.nombre }}</td>
              <td>{{ dato.descripcion }}</td>
              <td>${{ dato.importe }}</td>
              <td>{{ dato.fecha }}</td>
            </tr>
            <tr :style="{ color: calcularTotal.color }">
              <td>TOTAL</td>
              <td>${{ calcularTotal.total }}</td>
            </tr>
          </table>
        </div>
        <h5 v-else class="alert alert-warning">No hay datos ingresados</h5>

        <br />
      </vue-form>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-componentes-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      formState: {},
      formData: this.getInitialData(),
      nombreMinLength: 3,
      nombreMaxLength: 15,
      descripcionMinLength: 2,
      importeMin: 1,
      importeMax: 9999999999,
      datos: [],
      presupuesto: null,
    };
  },
  methods: {
    getInitialData() {
      return {
        nombre: null,
        descripcion: null,
        importe: null,
        fecha: null,
      };
    },
    enviar() {
      let ingreso = {...this.formData}
      ingreso.fecha = new Date().toLocaleString()
      this.datos.push(ingreso)

      this.formData = this.getInitialData();
      this.formState._reset();
    },
  },
  computed: {
    calcularTotal() {
      let total = 0;
      let color;
      this.datos.forEach((dato) => (total += dato.importe));
      if (total <= 1000) color = "#85f55f";
      if (total > 1000 && total <= 5000) color = "#a25ffa";
      if (total > 5000) color = "#de691b";
      return {
        total,
        color,
      };
    },

    getColorPresupuesto() {
      let total = 0;
      let color;
      this.datos.forEach((dato) => (total += dato.importe));
      if (total > this.presupuesto) color = "#d41515";

      return color;
    },
  },
};
</script>

<style scoped lang="css">
.jumbotron {
  background-color: rgb(196, 196, 196);
}
</style>
