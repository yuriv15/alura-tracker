<template>
    <main
        class="columns is-gapless is-multiline"
        :class="{ 'modo-escuro': modoEscuroAtivo }"
    >
        <div class="column is-one-quarter">
            <BarraLateral @aoTemaAlterado="trocarTema" />
        </div>
        <div class="column is-three-quarter conteudo">
            <FormularioComp @aoSalvarTarefa="salvarTarefa" />
            <div class="lista">
                <TarefaComp
                    v-for="(tarefa, index) in tarefas"
                    :key="index"
                    :tarefa="tarefa"
                />
                <BoxComp v-if="listaEstaVazia">
                    Você não está muito produtivo hoje :(
                </BoxComp>
            </div>
        </div>
    </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BarraLateral from '@/components/BarraLateral.vue'
import FormularioComp from '@/components/Formulario.vue'
import TarefaComp from '@/components/Tarefa.vue'
import iTarefa from '@/interfaces/iTarefa'
import BoxComp from '@/components/Box.vue'

export default defineComponent({
    name: 'App',
    components: { BoxComp, TarefaComp, FormularioComp, BarraLateral },
    data() {
        return {
            tarefas: [] as iTarefa[],
            modoEscuroAtivo: false,
        }
    },
    computed: {
        listaEstaVazia(): boolean {
            return this.tarefas.length === 0
        },
    },
    methods: {
        salvarTarefa(tarefa: iTarefa) {
            this.tarefas.push(tarefa)
        },
        trocarTema(modoEscuroAtivo: boolean) {
            this.modoEscuroAtivo = modoEscuroAtivo
        },
    },
})
</script>

<style lang="scss">
.lista {
    padding: 1.25rem;
}

main {
    --bg-primario: #fff;
    --texto-primario: #000;

    &.modo-escuro {
        --bg-primario: #2b2d42;
        --texto-primario: #ddd;
    }
}

.conteudo {
    background-color: var(--bg-primario);
}
</style>
