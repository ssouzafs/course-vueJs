<template>
    <input ref="inputRef" type="text" />
</template>

<script setup>
import { useCurrencyInput } from 'vue-currency-input';
const { inputRef } = useCurrencyInput(props.options)
const props = defineProps({
    modelValue: Number,
    options: Object
})


// export default {
//     name: 'CurrencyInput',
//     props: {
//         modelValue: Number, // Vue 2: value
//         options: Object
//     },
//     setup(props) {
//         const { inputRef } = useCurrencyInput(props.options)

//         return { inputRef }
//     }
// }
</script>