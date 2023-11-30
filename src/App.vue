<script setup>
import { reactive } from 'vue';

const nome = "miguel"

//let contador = 0
const estado = reactive({
  contador: 0,
  email: '',
  saldo: 5000,
  transferido: 0,
  nomes: ['andré', 'pedro', 'julia', 'maria'],
  inserirNome: '',
})

function incrementar() {
  estado.contador++;
}

function decrementar() {
  estado.contador--;
}

function alteraEmail(evento) {
  estado.email = evento.target.value;
}

function mostraSaldoRestante() {
  const { saldo, transferindo } = estado;
  return saldo - transferindo;
}

function validaValorTransferencia() {
  const { saldo, transferindo } = estado;
  return saldo >= transferindo;
}

function cadastrarNome() {
  if (estado.inserirNome.length >= 3) {
    estado.nomes.push(estado.inserirNome)
  } else {
    alert("digite mais caracteres")
  }
  console.log(estado)
}

</script>

<template>
  <h1>{{ nome }}</h1>

  <hr>

  {{ estado.contador }}

  <button @onclick="incrementar" type="button">+</button>
  <button @onclick="decrementar" type="button">-</button>

  <br>
  <hr>

  {{ estado.email }}
  <input type="email" @keyup="alteraEmail">

  <br>
  <hr>

  Saldo: {{ estado.saldo }} <br>
  Transferindo: {{ estado.transferindo }} <br>
  Saldo depois da transferência: {{ mostraSaldoRestante() }} <br>
  <input :class="{ invalido: !validaValorTransferencia() }" class="campo" @keyup="evento => estado.transferindo = evento.target.value" type="number" placeholder="Quantia para transferir">
  <button v-if="validaValorTransferencia()">Transferir</button>
  <span v-else>Valor maior que o saldo</span>

  <br>
  <hr>

  <ul>
    <li v-for="nome in estado.nomes">
    {{ nome }}</li>
  </ul>
  <input @keyup="evento => estado.inserirNome = evento.target.value" type="text" placeholder="Digite um novo nome">
  <button @click="cadastrarNome" type="button">Cadastrar nome</button>
</template>

<style scoped>
.invalido {
  outline-color: red;
  border-color: red;
}

.campo {
  border: 2px solid #000;
}
</style>