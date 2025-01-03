<script setup>
    const props = defineProps(['CadastraTarefa', 'tarefaTemp', 'trocarFiltro', 'editatarefatemp'])
</script>

<template>
    <form @submit.prevent="props.CadastraTarefa">
        <div class="row">
            <div class="col">
                <input v-bind:value="props.tarefaTemp" @change="props.editatarefatemp"
                    required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="Todas">Todas tarefas</option>
                    <option value="Pendentes">Pendentes</option>
                    <option value="Finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>