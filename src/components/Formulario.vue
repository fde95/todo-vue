<script setup>

    const props = defineProps (['cadastraTarefa', 'tarefaTemporaria', 'trocarFiltro', 'edtaTarefaTemp'])

</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemporaria" @change="props.edtaTarefaTemp" required type="text" placeholder="Digite a nova tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="concluidas">Concluídas</option>
                    <option value="pendentes">Pendentes</option>
                </select>
            </div>
        </div>
    </form>
</template>