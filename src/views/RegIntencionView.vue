<template>
  <div class="container">
    <h2>Registro de intenciones</h2>
    <b-form @reset="cerrar()">
      <b-form-group id="input-group-1" label="Intencion:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="intencion.intencion"
          type="text"
          placeholder="Escriba su intencion"
          required
        >
        </b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Ofrenda:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="intencion.ofrenda"
          type="number"
          placeholder="Valor de la ofrenda"
          required
        >
        </b-form-input>
      </b-form-group>
      <b-form-group id="input-group-2" label="Ofrece:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="intencion.remite"
          type="text"
          placeholder="Familia o persona quien ofrece la intencion"
          required
        >
        </b-form-input>
      </b-form-group>
    </b-form>
  </div>
</template>

<script>

export default {
  name: "RegIntencionView",
  components:{
  },
  data(){
    return{
        intencion:{
            id:0,
            intencion:"",
            ofrenda:10,
            remite:'',
            idmisa:0
        }
    }
  }
};
</script>

<style></style>
