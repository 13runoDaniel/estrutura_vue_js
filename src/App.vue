<script setup>
import { reactive } from 'vue';

// MOUSTACHE - <h1>{{  }}</h1>
const nome = "Bruno Daniel";

const meuObj = {
  nome: 'Bruno',
  gato: 'Perry'
}

function dizOla() {
  return `${nome} diz oi!!`
}

function nomeDogato() {
  return `O nome do gato é ${meuObj.gato}`
}

// V-BIND - <img v-bind:src="" alt="">
const enderecoLink = "https://upload.wikimedia.org/wikipedia/pt/thumb/1/10/Link_arte_Hyrule_Warriors_Age_of_Calamity.png/270px-Link_arte_Hyrule_Warriors_Age_of_Calamity.png"

// V-BIND - <img :src="" alt="">
const enderecoZelda = "https://upload.wikimedia.org/wikipedia/pt/thumb/7/7d/Princesa_Zelda_arte_Hyrule_Warriors_Age_of_Calamity.png/270px-Princesa_Zelda_arte_Hyrule_Warriors_Age_of_Calamity.png"

// DISABLED - :disabled
const botaoEstaHabilitado = false

// V-IF - v-if=""
const enderecoSidon = "https://upload.wikimedia.org/wikipedia/en/2/28/Prince_Sidon_from_Zelda.png?20210907085500"
const gostaDoSidon = true

// V-SHOW - v-show=""
const enderecoGanon = "https://upload.wikimedia.org/wikipedia/pt/thumb/8/8d/Ganon_render_Hyrule_Warriors_Legends.png/270px-Ganon_render_Hyrule_Warriors_Legends.png"
const gostaDoGanon = true

// V-IF V-ELSE-IF V-ELSE - v-else-if=""
const enderecoBreathOfTheWild = "https://upload.wikimedia.org/wikipedia/pt/thumb/0/0f/Legend_of_Zelda_Breath_of_the_Wild_capa.png/270px-Legend_of_Zelda_Breath_of_the_Wild_capa.png"
const tenhoBreathOfTheWild = true
const enderecoTearsOfTheKingdom = "https://upload.wikimedia.org/wikipedia/pt/thumb/2/25/Zelda_TotK_capa.jpg/270px-Zelda_TotK_capa.jpg"
const tenhoTearsOfTheKingdom = true

const estaAutorizado = false

// REACTIVE - variavel nome = reactive({ variavel: valorVariavel })
const estado = reactive({
  contador: 0,
  // @KEYUP - @keyup=""
  email: "",
  saldo: 5000,
  transferindo: 0,
  // V-FOR - v-for="parametro in variavel"
  nomes: ["Bruno", "Perry", "Eliana", "Oswaldo"],
  nomeInformado: ""
})

// @CLICK - @click=""
function incrementar() {
  estado.contador++
}

function decrementar() {
  estado.contador--
}

function alterarEmail(evento) {
  estado.email = evento.target.value
}

function mostrarSaldoFuturo() {
  const { saldo, transferindo } = estado

  return saldo - transferindo
}

function validarValorDeTransferencia() {
  const { saldo, transferindo } = estado

  return saldo >= transferindo
}

function cadastrarNome() {
  if (estado.nomeInformado.length >=3) {
    estado.nomes.push(estado.nomeInformado)
  } else {
      alert('Informe o nome superior a 2 caracteres')
    }
}

</script>


<template>

  <h1>{{ nome }}</h1> <br><hr>
  <h2>{{ meuObj }}</h2> <br>
  <h2>{{ meuObj.gato }}</h2> <br><hr>
  <h3>{{ dizOla() }}</h3> <br>
  <h3>{{ nomeDogato() }}</h3> <br><hr>

  <img v-bind:src="enderecoLink" alt=""> <br>
  <img :src="enderecoZelda" alt=""> <br><hr>

  <button :disabled="!botaoEstaHabilitado">Enviar mensagem</button> <br><hr>
  
  <!-- DIRETIVA -->
  <img v-if="gostaDoSidon" :src="enderecoSidon" alt=""> <br>
  <img v-show="!gostaDoGanon" :src="enderecoGanon" alt=""> <br><hr>
  <img v-if="tenhoBreathOfTheWild" :src="enderecoBreathOfTheWild" alt="">
  <img v-else-if="!tenhoTearsOfTheKingdom" :src="enderecoTearsOfTheKingdom" alt="">
  <h4 v-else>Não tenho nenhum Zelda</h4>
  <br><hr>
  <h5 v-if="estaAutorizado">Bem vindo</h5>
  <h5 v-else>Não entre</h5>
  <br><hr>

{{ estado.contador }}
<button type="button" @click="incrementar">+</button>
<button type="button" @click="decrementar">-</button>
<br><hr>
{{ estado.email }}
<input type="email" name="" id="" @keyup="alterarEmail"> <br><hr>

Saldo: {{ estado.saldo }} <br>
Transferindo {{ estado.transferindo }} <br>
Saldo depois da transferência: {{ mostrarSaldoFuturo() }} <br>
<input class="campo" :class="{ invalido: !validarValorDeTransferencia() }" type="number" name="" id="" placeholder="Quantia para transferir" @keyup="evento => estado.transferindo = evento.target.value">
<button v-if="validarValorDeTransferencia()" type="button">Transferir</button>
<span v-else>Valor maior que o saldo</span> <br><hr>

<ul>
  <li v-for="nome in estado.nomes">
    {{ nome }}
  </li>
</ul>
<input type="text" name="" id="" placeholder="Informe o novo nome" @keyup="evento => estado.nomeInformado = evento.target.value">
<button type="button" @click="cadastrarNome">Cadastrar nome</button>
<h1 v-for="nome in estado.nomes">{{ nome }}</h1>
</template>

<style scoped>

img {
  max-width: 200px;
}

/* CLASS - :class="{ styleClasse }" */
.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  border: 2px solid black;
}

</style>
