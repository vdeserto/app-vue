<template>
  <div class="center">
    <h3>Cadastrar Endereço</h3>
    
      <b-form @submit="onSubmit" @reset="onReset" v-if="show"> 
    <div class="form">
        <input v-model="form.cep" name="cep" autocomplete="off" required @change="onSubmit">
        <label for="cep" class="label">
          <span class="content">CEP</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.logradouro" name="logradouro" required>
        <label for="logradouro" class="label">
          <span class="content">Logradouro</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.complemento" name="complemento">
        <label id="complemento" class="label">
          <span class="content">Complemento</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.bairro" name="bairro" required>
        <label for="bairro" class="label">
          <span class="content">Bairro</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.localidade" name="localidade" required>
        <label for="localidade" class="label">
          <span class="content">Cidade</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.uf" name="uf" required>
        <label for="uf" class="label">
          <span class="content">Estado</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.ddd" name="ddd" required disabled>
        <label for="ddd" class="label">
          <span class="content">DDD</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.ibge" name="ibge" required disabled>
        <label for="ibge" class="label">
          <span class="content">Cód. IBGE</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.gia" name="gia" required disabled>
        <label for="gia" class="label">
          <span class="content">Cód. GIA</span>
        </label>
    </div>
    <div class="form">
        <input v-model="form.siafi" name="siafi" required disabled>
        <label for="siafi" class="label">
          <span class="content">Cód. SIAFI</span>
        </label>
    </div>
    
    <b-container>
      <b-row>
        <b-col>
        <b-button type="submit" variant="primary">Enviar</b-button>
        </b-col>
        <b-col>
        <b-button type="reset" variant="danger">Limpar Campos</b-button>
        </b-col>
      </b-row>
    </b-container>

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

<style>

  body{
    height: 100vh;
    display: flex;
    justify-content: space-around;
    align-items: center;
    flex-direction: column;
    font-family: sans-serif;
  }

  .center{
    justify-content:center;
    align-items:center;
    flex-direction: column;
    margin: 2.5%;
  }

  .form {
    width: 75%;
    position: relative;
    height: 50px;
    overflow: hidden;
    left:10%;
  }

  .form input {
    width: 75vw;
    height: 100%;
    color: #595f6e;
    padding-top: 2.5%;
    border: none;
    outline: none;
  }

  .form label {
    position: absolute;
    bottom: 0px;
    left: 0%;
    width: 100%;
    height: 100%;
    pointer-events: none;
    border-bottom: 1px solid black;
  }

  .form label::after {
    content: "";
    position: absolute;
    left: 0%;
    bottom: -3px;
    height: 100%;
    width: 100%;
    border-bottom: 3px solid #5fa8de;
    transform: translateX(-100%);
    transition: transform 0.3 ease;
  }

  .content {
    position: absolute;
    bottom: 4px;
    left: 0px;
    transition: all 0.3s ease;
  }

  .form input:focus + .label .content, 
  .form input:valid + .label .content,
  .form input:disabled + .label .content{
    transform: translateY(-75%);
    font-size: 14px;
    color: #5fa8d3;
  }

  .form input:focus + .label::after, 
  .form input:valid + .label::after{
    transform: translateX(0%);
  }

  .col{
    justify-content: center;
    align-items: center;
    display: flex;
    margin: 2.5%
  }

  label#complemento::after {
    border:none;
  }

</style>
