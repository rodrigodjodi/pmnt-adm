<template>
  <div id="app">
    <div id="nav">
        <img src="piemonte.png" alt="logo piemonte">
        
    </div>
    <div>
      <label for="select-emp">Empreendimento:</label>
      <select id="select-emp" v-model="empreendimento">
          <option value="">Selecione...</option>
          <option value="bosc">BOSC Eco Residence</option>
      </select>
      <hr>
      <div v-if="unidades!==null">
      <h2>Quadro resumo</h2>
        <table>
          <tr>
            <th>Unidade</th>
            <th>Tipologia</th>
            <th>Contrato</th>
            <th>E-mail</th>
            <th>Kit</th>
            <th>Piso áreas secas</th>
            <th>Paredes cozinha</th>
            <th>Kit aquecedor</th>
          </tr>
          <tr v-for="(props, unidade) in unidades" :key="unidade">
            <td>{{unidade}}</td>
            <td>{{props.tipologia}}</td>
            <td>{{props.contrato}}</td>
            <td>{{props.email}}</td>
            <td>{{props.kit}}</td>
            <td>{{props.op2}}</td>
            <td>{{props.op3}}</td>
            <td>{{props.op4}}</td>
          </tr>
        </table>
      </div>
      <hr>
      <div v-if="unidades!==null">
        <h3>Reset unidade</h3>  
        <label for="">Número ap</label>
        <input type="text" v-model="unidade">
        <select v-model="tipologia">
          <option v-for="tipologia in tipologias"
            :key="tipologia" :value="tipologia">
            {{tipologia}}
          </option>
        </select>
        <button @click="novoApartamento">Cadastrar</button>
      </div>
    </div>

  </div>
</template>
<script>
import { db } from "./firebase";

export default {
  data() {
    return {
      unidade: "",
      tipologia: "",
      tipologias: ["2quartos", "3quartos", "duplex"],
      acabamentos: ["padrao", "classico", "contemporaneo"],
      contrato: "",
      cpf: "",
      empreendimento: "",
      unidades: null
    };
  },
  methods: {
    novoApartamento() {
      const empreendimento = db.ref("empreendimentos/" + this.empreendimento);
      empreendimento
        .child(this.unidade)
        .set({ tipologia: this.tipologia })
        .then(function() {
          return empreendimento.once("value");
        })
        .then(function(snapshot) {
          var data = snapshot.val();
          console.log(data);
        });
    }
  },
  watch: {
    empreendimento() {
      if (!this.empreendimento) return;
      const empreendimento = db.ref("empreendimentos/" + this.empreendimento);
      empreendimento.on("value", snapshot => {
        this.unidades = snapshot.val();
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
  background-color: #d6d6cb;
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

.logo {
  flex: 1;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
