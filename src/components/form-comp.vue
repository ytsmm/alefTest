<script setup>
    import {ref, computed, provide} from 'vue'
    import infoComp from './info-comp.vue'
    import childrenComp from './children-comp.vue'

    defineEmits(['show'])

    const data = ref({ name: '', age: ''})
    const children = ref([])
    let childNum = ref(0)

    const showBtn = computed(() => {
        return children.value.length <= 4 ? true : false
    })
    const addChild = () => {
        children.value.push({name: '', age: '', id: childNum.value})
        childNum.value++
    }
    const removeChild = (id) => {
        children.value = children.value.filter( el => el.id !== id )
    }
    provide('removeChild', removeChild)
</script>

<template>
    <form @submit.prevent>
        <info-comp v-model:name="data.name" v-model:age="data.age">Персональные данные</info-comp>
        <children-comp :show="showBtn" @add="addChild" :children="children"></children-comp>
        <button @click="$emit('show', data, children)">Сохранить</button>
    </form>
    
</template>

<style scoped lang="scss">
@import "../assets/styles/variables.scss";
@import "../assets/styles/elements.scss";

button {
    color: #ffff;
    text-align: center;
    font-family: $font;
    font-size: 14px;
    font-weight: 400;
    line-height: 24px;
    padding: 10px 20px;
    background: $button-color;
    border: none;
    border-radius: 100px;
    cursor: pointer;
    margin-top: 30px;
  }
</style>
