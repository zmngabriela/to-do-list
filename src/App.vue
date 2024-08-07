<!-- Npm init vue@latest
Cd .. /pastavue
Git init
Npm install
Npm run dev
Fazer commit e criar repositório no github e vincular ao projeto
Limpar as coisas do vue -->

<script setup>
  import { reactive } from "vue";
  import Head from './components/Head.vue';
  import Forms from './components/Forms.vue';
  import Todo from './components/Todo.vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
        titulo: 'Estudar VueJS',
        finalizada: false,
      },
      {
        titulo: 'Estudar React',
        finalizada: false,
      },
      {
        titulo: 'Estudar Backend',
        finalizada: true,
      },
    ]
  })

  const getTarefasPendentes = () => {
    // ! e a mesma coisa que tarefa.finalizada === false)
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  } // a gente poderia ja passar o length aqui pro pra retornar somente o numero de tarefas pendentes, mas vamos reaproveitar essa funcao pra outras paradas

  const getTarefasFinalizadas = () => {
    // ! e a mesma coisa que tarefa.finalizada === false)
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const { filtro } = estado;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas':
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
    <Head :tarefas-pendentes="getTarefasPendentes().length"></Head>
    <Forms :tarefa-temp="estado.tarefaTemp" :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" :cadastra-tarefa="cadastraTarefa" :trocar-filtro="evento => estado.filtro = evento.target.value"></Forms>
    <Todo :tarefas="getTarefasFiltradas()"></Todo>
  </div>
</template>
