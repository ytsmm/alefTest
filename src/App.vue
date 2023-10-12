<script setup>
  import {ref} from 'vue'
  import formComp from './components/form-comp.vue'
  import previewComp from './components/preview-comp.vue'

  const currentTab = ref('formComp')
  const tabs = { formComp, previewComp }
  const label = (tab) => {
    return tab == 'formComp' ? 'Форма' : 'Превью'
  }

  const info = ref({name: '', age: '', children: []})

  const showData = (data, children) => {
    info.value.name = data.name;
    info.value.age = data.age;
    info.value.children = children;
  }
</script>

<template>
  <div class="wrapper">
    <div class="top">
      <header>
        <img src="./assets/img/logo.png" alt="logo">
        <div class="links">
          <button v-for="(_, tab) in tabs" 
            @click="currentTab = tab" 
            :class="{active: currentTab === tab}" 
            :key="tab">
            {{ label(tab) }}
          </button>
        </div>
      </header>
      <main class="main">
        <keep-alive>
          <component :is="tabs[currentTab]"
          @show="showData"
          :data="info">
          </component>
        </keep-alive>
        
      </main>
    </div>
    <footer class="footer">
      <span class="footerText">all rights reserved</span>
    </footer>
  </div>
  
</template>

<style lang="scss">
@import "./assets/styles/variables.scss";
@import "./assets/styles/elements.scss";
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
  }
  .wrapper {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  .top {
    flex-grow: 1;
  }
  header {
    padding: 22px 51px;
    display: flex;
    align-items: center;
    border-bottom: 1px solid $header-border;
    gap: 432px;
    @media (max-width: 1100px) {
      gap: 0;
      justify-content: space-between;
    }
    @media (max-width: 400px) {
      padding: 22px 5px;
    }
    .links {
      display: flex;
      gap: 24px;
      & button {
        color: $secondary-color;
        font-family: $font;
        font-size: 14px;
        font-weight: 400;
        line-height: 24px;
        background: none;
        border: none;
        cursor: pointer;
        transition: $transition;
        &.active {
          color: $main-color;
        }
        &:hover {
          color: $main-color;
        }   
      }
    }
  }
  .main {
    max-width: 616px;
    margin: 0 auto;
    padding-top: 30px;
  }
  .footer {
    padding: 30px 0;
    background: $footer-bg;
    &Text {
      display: flex;
      align-items: center;
      justify-content: center;
      color: #000;
      font-family: $font;
      font-size: 13px;
      font-weight: 400;
    }
  }

</style>
