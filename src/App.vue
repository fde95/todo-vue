<script setup>
    import { reactive } from 'vue';
    import Cabecalho from './components/Cabecalho.vue';
    import Formulario from './components/Formulario.vue';
    import ListadeTarefas from './components/ListadeTarefas.vue';

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
        <Cabecalho :tarefaPendente="getTarefasPend().length"></Cabecalho>
        <Formulario :trocarFiltro="evento => estado.filtro = evento.target.value" :tarefaTemporaria ="estado.tarefatemp" :edtaTarefaTemp="evento => estado.tarefaTemporaria = evento.target.value" :cadastraTarefa="cadastraTarefa"></Formulario>
        <ListadeTarefas :tarefasPops="getTarefasFiltradas()"></ListadeTarefas>
    </div>
</template>

