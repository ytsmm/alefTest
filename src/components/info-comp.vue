<script setup>
  defineProps({name: String, age: String})
  defineEmits(['update:name', 'update:age'])
</script>

<template>
  <div class="personalData">
    <h1><slot></slot></h1>
    <input placeholder="Имя" :value="name" @input="$emit('update:name', $event.target.value)" required>
    <input type="number" placeholder="Возраст" :value="age" @input="$emit('update:age', $event.target.value)" required>
  </div>
</template>

<style scoped lang="scss">
@import "../assets/styles/variables.scss";
@import "../assets/styles/elements.scss";
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  .personalData {
    & h1 {
      @extend %h1;
      margin-bottom: 20px;
    }
    & input{
      @extend %input;
      &:first-of-type {
        margin-bottom: 10px;
      }
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
