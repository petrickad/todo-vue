<script setup>
const props = defineProps(['tarefas', 'filtro']);

const tarefasFiltradas = () => {
  if (props.filtro === 'pendentes') {
    return props.tarefas.filter(tarefa => !tarefa.finalizada);
  }
  return props.tarefas;
};

</script>

<template>
    <ul v-if="tarefasFiltradas().length > 0" class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in props.tarefas">
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
    <p v-else>Não possui nenhuma tarefa pendente</p>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}

</style>