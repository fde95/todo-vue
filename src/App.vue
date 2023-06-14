<script setup>
import { reactive } from 'vue';

const estado = reactive({
    filtro: 'todas',
    tarefatemp: '',
    tarefas: [
        {
            titulo : 'Estudar ES6',
            finalizado: false
        },
        {
            titulo : 'Estudar SASS',
            finalizado: false
        },
        {
            titulo : 'Estudar vueJS',
            finalizado: true
        }
    ]
})

const getTarefasPend = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizado)
}
const getTarefasFin = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizado)
}

const getTarefasFiltradas = () => {
    const {filtro} = estado;

    switch (filtro){
        case 'pendentes':
            return getTarefasPend();
        case 'concluidas':
            return getTarefasFin();
        default:
            return estado.tarefas;
    }
}

const cadastraTarefa = () => {
    const newTarefa = {
        titulo : estado.tarefatemp,
        finalizado: false
    }
    estado.tarefas.push(newTarefa);
    estado.tarefatemp = ''
}
</script>

<template>
    <div class="container">
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Minhas Tarefas</h1>
            <p>
                Você possui {{getTarefasPend().length}} tarefas pendentes
            </p>
        </header>
    <form @submit.prevent="cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="estado.tarefatemp" @change="evento => estado.tarefatemp = evento.target.value" required type="text" placeholder="Digite a nova tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="evento => estado.filtro = evento.target.value" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="concluidas">Concluídas</option>
                    <option value="pendentes">Pendentes</option>
                </select>
            </div>
        </div>
    </form>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
            <label :class="{done: tarefa.finalizado}" class="ms-3" :for="tarefa.titulo">
                {{tarefa.titulo}}
            </label>
        </li>
    </ul>
</div>
</template>

<style scoped>
.done{
    text-decoration: line-through;
    color: green;
}
</style>
