<script setup>
    import { inject } from 'vue'
    defineProps({name: String, age: String})
    defineEmits(['update:name', 'update:age'])
    const removeChild = inject('removeChild')
</script>

<template>
  <div class="child">
    <input placeholder="Имя" :value="name" @input="$emit('update:name', $event.target.value)" required>
    <input type="number" placeholder="Возраст" :value="age" @input="$emit('update:age', $event.target.value)" required>
    <button @click="removeChild(this.$.vnode.key)">Удалить</button>
  </div>
</template>

<style scoped lang="scss">
@import "../assets/styles/variables.scss";
@import "../assets/styles/elements.scss";
    .child {
        display: flex;
        align-items: center;
        margin-bottom: 10px;  
        @media (max-width: 768px) {
            flex-direction: column;
            align-items: start;
            margin-bottom: 30px;
        }
        gap: 18px;
        & input {
            @extend %input;
            width: 260px;
        }
        & button {
            font-family: $font;
            color: $button-color;
            background: #ffff;
            border: none;
            cursor: pointer;
            font-size: 14px;
            font-weight: 400;
            line-height: 24px;
        }
        input::-webkit-outer-spin-button,
        input::-webkit-inner-spin-button {
            -webkit-appearance: none;
            margin: 0;
        }
        input[type=number] {
            appearance: textfield;
        }
    }
</style>
