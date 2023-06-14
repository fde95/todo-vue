<script setup>

    const props = defineProps(['tarefasPops']);

</script>

<template>
        <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefasPops">
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" 
            :id="tarefa.titulo" type="checkbox">
            <label :class="{done: tarefa.finalizado}" class="ms-3" :for="tarefa.titulo">
                {{tarefa.titulo}}
            </label>
        </li>
    </ul>
</template>