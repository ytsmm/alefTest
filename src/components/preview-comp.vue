<script setup>
defineProps({data: Object})
defineEmits(['show'])
</script>

<template>
    <div class="preview">
        <div class="personal">
            <h1>Персональные данные</h1>
            <span class="info">{{ data.name }} {{ data.age }}</span>
        </div>

        <div class="children">
            <h1>Дети</h1>
            <span v-for="child in data.children" :key="child.id" class="info">{{ child.name }}, {{ child.age }}</span>
        </div>
    </div>
</template>

<style scoped lang="scss">
@import "../assets/styles/variables.scss";
@import "../assets/styles/elements.scss";

    .personal {
        display: flex;
        gap: 20px;
        flex-direction: column;
        margin-bottom: 60px;
        & h1 {
            @extend %h1;
        }
        & .info {
            @extend %info;
        }
}
    .children {
        display: flex;
        flex-direction: column;
        gap: 20px;
        & h1 {
            @extend %h1;
        }
        & .info {
            @extend %info;
            background: $el-bg;
            padding: 10px 20px;
            border-radius: 5px;
        }
    }
</style>
