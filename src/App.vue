<script setup>
  import { reactive } from 'vue';
  import Cabecalho from './components/Cabecalho.vue'
  import Formulario from './components/Formulario.vue'
  import ListaDeTarefas from './components/ListasDeTarefas.vue'

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar SASS',
        finalizada: false,
      },
      {
        titulo: 'Estudar Vue',
        finalizada: true,
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === false)
  }

  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada === true)
  }

  const getTarefasFiltradas = () => {
    const filtro = estado.filtro;

    switch (filtro) {
      case 'Pendentes':
        return getTarefasPendentes();
      case 'Finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho v-bind:tarefas-pendentes="getTarefasPendentes().length"/>
    <Formulario v-bind:trocar-filtro="evento => estado.filtro = evento.target.value" v-bind:tarefa-temp="estado.tarefaTemp" v-bind:edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" v-bind:-cadastra-tarefa="cadastraTarefa"/>
    <ListaDeTarefas v-bind:tarefas="getTarefasFiltradas()"/>
  </div>
</template>

