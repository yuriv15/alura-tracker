<template>
    <div class="column is-flex is-align-items-center">
        <CronometroComp :tempoEmSegundos="tempoEmSegundos" />
        <div class="ml-5">
            <BotaoComp
                label="play"
                icone="fas fa-play"
                @click="iniciar"
                v-if="!cronometroRodando"
            />
            <BotaoComp
                label="stop"
                icone="fas fa-stop"
                @click="finalizar"
                v-else
            />
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import CronometroComp from '@/components/Cronometro.vue'
import BotaoComp from '@/components/Botao.vue'

export default defineComponent({
    name: 'TemporizadorComp',
    emits: ['aoTemporizadorFinalizado'],
    components: { BotaoComp, CronometroComp },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false,
        }
    },
    methods: {
        iniciar() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos++
            }, 1000)
        },

        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        },
    },
})
</script>
