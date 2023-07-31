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
    <button :class="[colorClass[props.color], {
        'rounded-l-full ml-2 my-2': props.display === '',
        'rounded-r-full mr-2 my-2': props.display === '0',
        'rounded-full m-2': !!props.display && props.display !== '0'
    }]" class="aspect-square duration-100">
        <p class="text-3xl font-mono">{{ props.display }}</p>
    </button>
</template>