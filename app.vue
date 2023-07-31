<script setup lang="ts">

interface Button {
  display: string,
  calculation: string,
  color: ButtonColor
}

const result = ref('')
const calculation = ref<Button[]>([])
const displayString = computed(() => calculation.value.map(v => v.display).join(''))
const calculationString = computed(() => calculation.value.map(v => v.calculation).join(''))
function calculate(value: typeof buttons[number]) {

  if (value.calculation === 'remove_last') {
    calculation.value = calculation.value.slice(0, -1)
    return
  }

  if (value.calculation === 'AC') {
    calculation.value = []
    result.value = ''
    return
  }

  if (value.calculation === '=') {
    result.value = +eval(calculationString.value).toFixed(6) + ''
    return
  }
  result.value = ''

  calculation.value.push(value)
}

const buttons = [
  {
    display: 'AC',
    calculation: 'AC',
    color: 'light',
  },
  {
    display: '±',
    calculation: '±',
    color: 'light',
  },
  {
    display: '%',
    calculation: '%',
    color: 'light',
  },
  {
    display: '÷',
    calculation: ' / ',
    color: 'highlight',
  },
  {
    display: '7',
    calculation: '7',
    color: 'default'
  },
  {
    display: '8',
    calculation: '8',
    color: 'default'
  },
  {
    display: '9',
    calculation: '9',
    color: 'default'
  },
  {
    display: '×',
    calculation: ' * ',
    color: 'highlight'
  },
  {
    display: '4',
    calculation: '4',
    color: 'default'
  },
  {
    display: '5',
    calculation: '5',
    color: 'default'
  },
  {
    display: '6',
    calculation: '6',
    color: 'default'
  },
  {
    display: '-',
    calculation: ' - ',
    color: 'highlight'
  },
  {
    display: '1',
    calculation: '1',
    color: 'default'
  },
  {
    display: '2',
    calculation: '2',
    color: 'default'
  },
  {
    display: '3',
    calculation: '3',
    color: 'default'
  },
  {
    display: '+',
    calculation: ' + ',
    color: 'highlight'
  },
  {
    display: '<',
    calculation: 'remove_last',
    color: 'highlight'
  },
  {
    display: '0',
    calculation: '0',
    color: 'default'
  },
  {
    display: ',',
    calculation: '.',
    color: 'default'
  },
  {
    display: '=',
    calculation: '=',
    color: 'highlight'
  },
] as const satisfies readonly Button[]

useHead({
  htmlAttrs: {
    class: 'bg-gray-800'
  }
})
</script>

<template>
  <div class="mx-auto max-w-md h-[100dvh] flex flex-col justify-end ">
    <div class="text-6xl flex justify-end items-end h-40 p-4 font-mono text-white">
      <span v-if="!result && !displayString">0</span>
      <span v-else-if="result">{{ result }}</span>
      <span v-else>{{ displayString }}</span>
    </div>
    <div class="grid grid-cols-4 p-2">
      <CalculatorButton v-for="item of buttons" @click="calculate(item)" :color="item.color" :display="item.display" />
    </div>
  </div>
</template>
