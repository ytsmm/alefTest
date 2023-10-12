<script setup>
    import childComp from './child-comp.vue'
    
    defineProps({children: Array, show: Boolean})
    defineEmits(['children:name', 'add'])
</script>

<template>
    <div class="children">
        <div class="header">
            <h1>Дети (макс. 5)</h1>
            <button v-show="show" @click="$emit('add')"><i class="fa-solid fa-plus"></i>Добавить ребенка</button>
        </div>
        <child-comp v-for="child in children" :key="child.id" v-model:name="child.name" v-model:age="child.age"></child-comp>
    </div>
</template>

<style scoped lang="scss">
@import "../assets/styles/variables.scss";
@import "../assets/styles/elements.scss";
    .children {
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            min-height: 44px;
            margin: 33px 0 11px;
            & button {
                border-radius: 100px;
                border: 2px solid $button-color;
                color: $button-color;
                background: #ffff;
                padding: 10px 20px;
                cursor: pointer;
                display: flex;
                gap: 8px;
                transition: $transition;
                font-family: $font;
                & i {
                    font-size: 18px;
                }
                &:hover {
                    color: #ffff;
                    background: $button-color;
                }
            }
        }
        & h1 {
            @extend %h1;
        }
    }
</style>
