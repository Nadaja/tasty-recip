<template>
<div>
<div>
<web-header></web-header>
<router-view></router-view>
<web-footer></web-footer>

</div>
</div>
</template>

<script setup>
    import { RouterView } from 'vue-router'
    import WebHeader from './components/header/WebHeader.vue'
    import WebFooter from "./components/footer/WebFooter.vue"
</script>