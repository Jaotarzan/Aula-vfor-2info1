<script setup>
import { ref, reactive, onMounted } from 'vue'

const cidades = ref([
    'São Paulo',
    'Rio de Janeiro',
    'Belo Horizonte',
    'Salvador',
    'Fortaleza',
    'Curitiba',
    'Manaus',
    'Recife',
    'Porto Alegre',
    'Brasília'
])

const cidadeNova = ref('')

function adicionarCidade() {
  if (cidadeNova.value != "") {
    cidades.value.push(cidadeNova.value)
    cidadeNova.value = ""
  } 
}

</script>

<template>
 <div class="cidades">
  <h1>lista de cidades</h1>
  <ul>
    <li v-for="(cidade, key) in cidades.sort()" :key="key">{{ cidade }}</li>
  </ul>
  <label>Informe se deseja adicionar cidades:</label>
  <div>
  <input type="text" v-model="cidadeNova" >
</div>  
  <button @click="adicionarCidade">adicionar cidade</button>
 </div>
</template>

<style scoped>

</style>