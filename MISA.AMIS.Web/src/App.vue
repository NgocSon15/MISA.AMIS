<template>
  <div id="app">
    <Navbar/>
    <Header/>
    <Content/>
  </div>
</template>

<script>
import Navbar from './components/layout/Navbar.vue'
import Header from './components/layout/Header.vue'
import Content from './components/layout/Content.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    Header,
    Content,
  }
}
</script>

<style>
#app {
    font-size: 13px;
    font-family:'NotoSans-Regular';
}

@font-face {
    font-family: 'NotoSans-Regular';
    src: url('assets/fonts/notosans-regular.2cb88a13.woff2');
}

@font-face {
    font-family: 'NotoSans-Bold';
    src: url('assets/fonts/notosans-bold.3ede5aff.woff2');
}

@font-face {
    font-family: 'NotoSans-Italic';
    src: url('assets/fonts/notosans-italic.1c1aaac9.woff2');
}

@font-face {
    font-family: 'NotoSans-SemiBold';
    src: url('assets/fonts/notosans-semibold.df3e6dc4.woff2');
}

::-webkit-scrollbar {
    width: 5px !important;
    height: 5px !important;
    background-color: #e9ebee;
}

::-webkit-scrollbar-thumb {
    width: 5px;
    height: 5px;
    background-color: #bbbbbb;
}

::placeholder {
    font-style: italic;
}           

.filter {
    height: 32px;
    width: 220px;
    border: 1px solid #e9ebee;
    display: flex;
    align-items: center;
    border-radius: 5px;
    margin-right: 24px;
}

.text-box {
    outline: none;
    height: 30px;
    border: 1px solid #e5e5e5;
    border-radius: 5px;
    border-left: none;
    border-right: none;
    padding-left: 12px;
}

.icon-search {
    background: url('assets/img/Sprites.64af8f61.svg') no-repeat -984px -352px;
    width: 32px;
    height: 32px;
}
</style>
