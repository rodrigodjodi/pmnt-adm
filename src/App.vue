<template>
  <div id="app">
    <div id="nav">
        <img src="piemonte.png" alt="logo piemonte">
      <div class="login">ATUALIZAR</div>
    </div>
  <div>
    <label for="">Número ap</label>
    <input type="text" v-model="unidade">
    <select v-model="tipologia">
      <option v-for="tipologia in tipologias"
        :key="tipologia" :value="tipologia">
        {{tipologia}}
      </option>
    </select>
  </div>
  </div>
</template>
<script>
import {unidades} from './firebase'

export default {
  data () {
    return {
      unidade: "",
      tipologia: "",
      tipologias: ["2quartos", "3quartos", "duplex"],
      acabamentos: ["padrao", "classico", "contemporaneo"],
      contrato: "",
      cpf: ""
    }
  },
  methods: {
    novoApartamento(numero, tipologia) {
      unidades.child(numero).set({tipologia: tipologia})
      .then(function() {
        return unidades.once("value");
      })
    .then(function(snapshot) {
      var data = snapshot.val();
      console.log(data)
    });
    }
  }
};
</script>

<style>
h2,
h3 {
  font-weight: 300;
}
html,
body {
  background-color: #2d2d2b;
  margin: 0;
}
#app {
  font-family: "Lato", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
#nav {
  display: flex;
  background-color: rgba(69, 82, 88, 0.9);
  padding: 10px 20px;
  border-bottom: 1px solid #455258;
  align-items: center;
}
#nav img {
  width: 200px;
  height: 49px;
}
.login {
  margin-left: auto;
  color: white;
  text-decoration: none;
  color: #42b983;
  cursor: pointer;
}
.logo {
  flex: 1;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
