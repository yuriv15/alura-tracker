<template>
    <div class="box formulario">
        <div class="columns">
            <div
                class="column is-8"
                role="form"
                aria-label="Formulário para criação de uma nova tarefa"
            >
                <input
                    type="text"
                    class="input"
                    placeholder="Qual tarefa você deleja iniciar?"
                    v-model="descricao"
                />
            </div>
            <TemporizadorComp @aoTemporizadorFinalizado="finalizarTarefa" />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TemporizadorComp from '@/components/Temporizador.vue'

export default defineComponent({
    name: 'FormularioComp',
    emits: ['aoSalvarTarefa'],
    components: { TemporizadorComp },
    data() {
        return {
            descricao: '',
        }
    },
    methods: {
        finalizarTarefa(tempoDecorrido: number) {
            this.$emit('aoSalvarTarefa', {
                duracaoEmSegundos: tempoDecorrido,
                descricao: this.descricao,
            })
            this.descricao = ''
        },
    },
})
</script>

<style lang="scss">
.formulario {
    color: var(--texto-primario);
    background-color: var(--bg-primario);
}
</style>
