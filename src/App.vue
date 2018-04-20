<template>
  <div id="app">
    <div id="nav">
        <img src="piemonte.png" alt="logo piemonte">
      <div class="login">ATUALIZAR</div>
    </div>
  </div>
</template>
<script>
import {unidades} from './firebase'
unidades.set({"101": {
                tipologia: '2quartos',
                acabamento: 'padrao'
              }
})
  .then(function() {
   return unidades.once("value");
  })
  .then(function(snapshot) {
    var data = snapshot.val();
    console.log(data)
    // data is { "name": "Ada", "age": 36 }
    // data.name === "Ada"
    // data.age === 36
  });
export default {

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
