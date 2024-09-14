<script setup>
  import { reactive } from 'vue';

const estado = reactive({
  valor1: 0,
  valor2: 0,
  filtro: "adicao",
  resultado: 0,
})

function trocaFiltro(evento){
  estado.filtro = evento.target.value;
  calcula()
}

function getValor1(evento){
  estado.valor1 = parseInt(evento.target.value);
  calcula()
}
function getValor2(evento){
  estado.valor2 = parseInt(evento.target.value);
  calcula()
}
function soma(){
  return estado.resultado = estado.valor1 + estado.valor2;
}
function subtracao(){
  return estado.resultado = estado.valor1 - estado.valor2;
}
function divisao(){
  return estado.resultado = estado.valor1 / estado.valor2;
}
function multiplicacao(){
  return estado.resultado = estado.valor1 * estado.valor2;
}

function calcula(){
  const {filtro} = estado;

  switch(filtro){
    case "adicao":
      return soma();
    case "subtracao":
      return subtracao();
    case 'divisao':
      return divisao();
    case 'multiplicacao':
      return multiplicacao();
    default:
      return 0;
  }
}
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-secondary">
      <h1 class="">Calculadora</h1>
    </header>
    <form @submit="">
      <div class="row">
        <div class="col-1">
          <input @input="getValor1" @keyup="getValor1" required class="form-control" type="number">
        </div>
        <div class="col-1">
          <input @input="getValor2" @keyup="getValor2" required class="form-control" type="number">
        </div>
        <div class="col-2">
          <select @change="trocaFiltro" class="form-control">
            <option value="adicao">Adição</option>
            <option value="subtracao">Subtração</option>
            <option value="divisao">Divisão</option>
            <option value="multiplicacao">Multiplicação</option>
          </select>
        </div>
        <div class="col-1 ms-5 list-group">
          <span class="list-group-item" >{{ estado.valor1 }}</span>
        </div>
          <span v-if="estado.filtro === 'adicao'" class="col-1 list-group-item text-center">+</span>
          <span v-else-if="estado.filtro === 'subtracao'" class="col-1 list-group-item text-center">-</span>
          <span v-else-if="estado.filtro === 'divisao'" class="col-1 list-group-item text-center">/</span>
          <span v-else-if="estado.filtro === 'multiplicacao'" class="col-1 list-group-item text-center">*</span>
        <div class="col-1 list-group">
          <span class="list-group-item" >{{ estado.valor2 }}</span>
        </div>
        <div class="col ms-5 list-group">
          <span class="list-group-item" >Resultado: {{ estado.resultado }}</span>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped>
header {
  color: #fff;
  border-radius: 24px;
  text-align: center;
}
.list-group-item{
  padding: 6px 12px;
}

</style>
