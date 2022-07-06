<template>
    <BoxComp>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroComp :tempoEmSegundos="tarefa.duracaoEmSegundos" />
            </div>
        </div>
    </BoxComp>
</template>

<script lang="ts">
import CronometroComp from '@/components/Cronometro.vue'
import { defineComponent, PropType } from 'vue'
import iTarefa from '../interfaces/iTarefa'
import BoxComp from '@/components/Box.vue'

export default defineComponent({
    name: 'TarefaComp',
    components: { BoxComp, CronometroComp },
    props: {
        tarefa: {
            type: Object as PropType<iTarefa>,
            required: true,
        },
    },
})
</script>

<style lang="scss" scoped></style>
