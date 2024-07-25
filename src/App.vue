<script setup>
import { reactive } from "vue";

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
  } // a gente poderia ja passar o lenght aqui pro pra retornar somente o numero de tarefas pendentes, mas vamos reaproveitar essa funcao pra outras paradas

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" required @change="evento => estado.tarefaTemp = evento.target.value" type="text" placeholder="Digite aqui a descriçao da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button class="btn btn-primary" type="submit">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => evento.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()" :key="tarefa.titulo">
        <!-- pra fazer checkbox selecionar quando a finalizada for true: -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <!-- pra fazer a classe done ser valida somente quando a tarefa e finalizada for true **o === true e opcional  -->
        <label :class="{ done: tarefa.finalizada === true }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
