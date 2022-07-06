<template>
    <button class="button" @click="$emit('click')">
        <span class="icon">
            <i :class="icone"></i>
        </span>
        <span>{{ label }}</span>
    </button>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'BotaoComp',
    emits: ['click'],
    props: {
        label: {
            type: String,
            required: true,
        },
        icone: {
            type: String,
            required: true,
        },
    },
})
</script>

<style lang="scss" scoped></style>
