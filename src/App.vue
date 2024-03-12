<script setup>
import { ref, computed } from 'vue'

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

const CidadesOrdenadas = computed(() => {
  return cidades.value.sort()
})

const cidadeNova = ref('')

function adicionarCidade() {
  if (cidadeNova.value != '') {
    cidades.value.push(cidadeNova.value)
    cidadeNova.value = ''
  }
}

function excluirCidade(i) {
  cidades.value.splice(cidades.value.indexOf(i), 1)
}
</script>

<template>
  <div class="cidades">
    <h1>lista de cidades</h1>
    <ul>
      <li v-for="(cidade, key) in CidadesOrdenadas" :key="key">
       <p> {{ cidade }} </p>
        <button @click="excluirCidade(cidade)">excluir</button>
      </li>
    </ul>
    <label>Informe se deseja adicionar cidades:</label>
    <div>
      <input type="text" v-model="cidadeNova" />
    </div>
    <button @click="adicionarCidade">adicionar cidade</button>
  </div>
</template>

<style scoped></style>