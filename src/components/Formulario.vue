<template>
  <div class="container col-6">
    <h3>Cadastrar Endereço</h3>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group label="Cep">
        <b-form-input v-model="form.cep" @change="onSubmit"></b-form-input>
      </b-form-group>

      <b-form-group label="Logradouro">
        <b-form-input v-model="form.logradouro"></b-form-input>
      </b-form-group>

      <b-form-group label="Complemento">
        <b-form-input v-model="form.complemento"></b-form-input>
      </b-form-group>

      <b-form-group label="Bairro">
        <b-form-input v-model="form.bairro"></b-form-input>
      </b-form-group>

      <b-form-group label="Localidade">
        <b-form-input v-model="form.localidade"></b-form-input>
      </b-form-group>

      <b-form-group label="uf">
        <b-form-input v-model="form.uf"></b-form-input>
      </b-form-group>

      <b-form-group label="ibge">
        <b-form-input v-model="form.ibge"></b-form-input>
      </b-form-group>

      <b-form-group label="gia">
        <b-form-input v-model="form.gia"></b-form-input>
      </b-form-group>

      <b-form-group label="ddd">
        <b-form-input v-model="form.ddd"></b-form-input>
      </b-form-group>

      <b-form-group label="siafi">
        <b-form-input v-model="form.siafi"></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      form: {
        cep: "",
        logradouro: "",
        complemento: "",
        bairro: "",
        localidade: "",
        uf: "",
        ibge: "",
        gia: "",
        ddd: "",
        siafi: "",
      },
      show: true,
    };
  },
  methods: {
    
    onSubmit() {
     //evt.preventDefault();
     // alert(JSON.stringify(this.form.cep));
      axios
        .get(`https://viacep.com.br/ws/` + this.form.cep + `/json/`)
        .then((response) => {
          console.log(response.data);
          this.form.cep = response.data.cep;
          this.form.logradouro = response.data.logradouro;
          this.form.complemento = response.data.complemento;
          this.form.bairro = response.data.bairro;
          this.form.localidade = response.data.localidade;
          this.form.uf = response.data.uf;
          this.form.ibge = response.data.ibge;
          this.form.gia = response.data.gia;
          this.form.ddd = response.data.ddd;
          this.form.siafi = response.data.siafi;
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
    onReset(evt) {
      evt.preventDefault();
      this.form.cep = "";
      this.form.logradouro = "";
      this.form.complemento = "";
      this.form.bairro = "";
      this.form.localidade = "";
      this.form.uf = "";
      this.form.ibge = "";
      this.form.gia = "";
      this.form.ddd = "";
      this.form.siafi = "";
    },
  },
};
</script>

<style scoped></style>
