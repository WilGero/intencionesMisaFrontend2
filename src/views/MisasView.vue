<template>
  <div class="container">
    <h2>MISAS</h2>
    <b-button variant="primary" @click="nuevo()">
      <b-icon-plus-circle></b-icon-plus-circle>
    </b-button>
    <b-modal id="modal-1" title="Misas" no-close-on-esc no-close-on-backdrop>
      <b-container fluid>
        <b-form @reset="cerrar()">
          <b-form-group
            id="input-group-1"
            label="Tipo de misa:"
            label-for="input-1"
          >
            <b-form-input
              id="input-1"
              v-model="misa.tipo"
              type="text"
              placeholder="Ingrese el tipo de misa"
              required
            >
            </b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-2"
            label="Fecha:"
            label-for="input-2"
          >
            <b-form-input
              id="input-2"
              v-model="misa.fecha"
              type="datetime-local"
              placeholder="Ingrese la fecha"
              required
            >
            </b-form-input>
          </b-form-group>
          
        </b-form>
      </b-container>
      <template #modal-footer="{}">
        <b-button size="sm" variant="danger" @click="cerrar()">Cancelar</b-button>
        <b-button size="sm" variant="success" @click="guardarMisa()">Guardar</b-button>
    </template>
    </b-modal>

    <b-table
      striped
      hover
      :items="misas"
      :fields="campos"
      stacked="md"
      show-empty
      small
    >
      <template #cell(actions)="row">
        <b-button
          variant="primary"
          size="sm"
          @click="modificar(row.item)"
          class="mr-1"
          >Modificar
        </b-button>
        <b-button
          variant="danger"
          size="sm"
          @click="borrarMisa(row.item)"
          class="mr-1"
          >Borrar
        </b-button>
      </template>
    </b-table>
  </div>
</template>
<script>
export default {
  name: "MisasView",
  data() {
    return {
      campos: [
        { key: "tipo", label: "Tipo de Misa" },
        { key: "fecha", label: "Fecha" },
        { key: "actions", label: "Opciones" },
      ],
      misas: [],
      misa: {
        id: 0,
        tipo: "",
        fecha: "",
      },
      accion:0
    };
  },
  methods: {
    cerrar(){
        this.$root.$emit("bv::hide::modal", "modal-1");
    },
    modificar(id) {
        this.misa=id;
        this.accion=1;
      this.$root.$emit("bv::show::modal", "modal-1");
    },
    nuevo() {
      this.$root.$emit("bv::show::modal", "modal-1");
    },
    async borrarMisa(id) {
      await this.axios.post("http://localhost:5000/misa/borrar", id);
      this.listarMisas();
    },
    async listarMisas() {
      await this.axios.get("http://localhost:5000/misa/").then((r) => {
        console.log(r.data.data);
        this.misas = r.data.data;
      });
    },
    async guardarMisa() {
      if(this.accion===0){
        await this.axios
        .post("http://localhost:5000/misa/agregar", this.misa)
        .then((r) => {
          this.misas.push(r.data.data);
          this.misa = {
            tipo: "",
            fecha: "",
          };
          this.listarMisas();
        })
        .catch((error) => {
          console.log(error);
        });
      }else{
        await this.axios
        .post("http://localhost:5000/misa/modificar", this.misa)
        .then((r) => {
          this.misas.push(r.data.data);
          this.listarMisas();
        })
        .catch((error) => {
          console.log(error);
        });
      }
      
    },
  },
  mounted() {
    this.listarMisas();
  },
};
</script>
