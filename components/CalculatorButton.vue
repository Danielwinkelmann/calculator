<script setup lang="ts">
const props = withDefaults(defineProps<{
    color?: ButtonColor
    display: string
}>(), {
    color: 'default'
})

const colorClass: Record<typeof props.color, string> = {
    default: 'bg-gray-100 hover:bg-gray-200 text-gray-800',
    light: 'bg-gray-700 hover:bg-gray-800 text-white',
    highlight: 'bg-orange-500 hover:bg-orange-600 text-white'
}
</script>

<template>
    <button :class="[colorClass[props.color]]" class="aspect-square duration-100 rounded-full m-2">
        <p class="text-3xl font-mono">{{ props.display }}</p>
    </button>
</template>