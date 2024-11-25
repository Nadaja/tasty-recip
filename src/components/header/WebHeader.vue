<template>
    <header
    class="shadow-sm container-fluid
    
    bg-white py-3 border-bottom fixed-top" >
    
    <div class="container-md d-flex
    
    justify-content-between align-items-center" >
    <img src="@/assets/images/Logo.png" alt="Logo" />
    <!-- Component NavigationBar -->
    <header-navbar>

    </header-navbar>
    </div>
    </header>
    </template>

    <script setup>
        import HeaderNavbar from"./NavigationBar.vue"
    </script>