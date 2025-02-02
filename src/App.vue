<script setup>
import {reactive} from 'vue'
import Headerapp from './components/Headerapp.vue'
import Formapp from './components/Formapp.vue'
import Listapp from './components/Listapp.vue'


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
        titulo: 'Ir para academia',
        finalizada: true,
      }
    ]
  })

  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro){
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
        return getTarefasFinalizadas();
      default:
        return estado.tarefas;
    }
  }
const cadastraTarefa = () => {
  console.log(estado.tarefaTemp)
  console.log("entrou")
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

    <Headerapp :tarefas-pendentes="getTarefasPendentes().length" />
    <Formapp 
      :trocar-filtro="evento => estado.filtro = evento.target.value" 
      :tarefa-temp="estado.tarefaTemp" 
      :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" 
      :cadastra-tarefa="cadastraTarefa" />
    <Listapp :tarefas="getTarefasFiltradas()"/>



</div>
</template>


