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

const edicao = ref(-1)
const cidadeNova = ref('')
const cidadeAlterada = ref('')
const cidadeOriginal = ref('')

function adicionarCidade() {
  if (cidadeNova.value != '') {
    cidades.value.push(cidadeNova.value)
    cidadeNova.value = ''
  }
}

function excluirCidade(i) {
  cidades.value.splice(cidades.value.indexOf(i), 1)
}

function editarCidade(i) {
  cidadeOriginal.value = i
  cidadeAlterada.value = cidades.value[cidades.value.indexOf(i)]
  edicao.value = cidades.value.indexOf(i)
}

function confirmarEdicao() {
  cidades.value.splice(cidades.value.indexOf(cidadeOriginal.value), 1, cidadeAlterada.value)
  edicao.value = -1
}

const CidadesOrdenadas = computed(() => {
  return cidades.value.sort()
})
</script>

<template>
  <div class="cidades">
    <h1>lista de cidades</h1>
    <ul>
      <li v-for="(cidade, key) in CidadesOrdenadas" :key="key">
        <p v-if="edicao != cidades.indexOf(cidade)">{{ cidade }}</p>
        <div v-else>
          <input type="text" v-model="cidadeAlterada" />
        </div>
        <button @click="excluirCidade(cidade)">excluir</button>
        <button @click="editarCidade(cidade)" v-if="edicao != cidades.indexOf(cidade)">
          editar
        </button>
        <button @click="confirmarEdicao" v-else>confirmar</button>
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
