<template>
    <div class="recipe__list-recipe row" >
    <recipe-card v-for = "(recipe, id) in recipes" :id=id :recipe = "recipe">
        
    </recipe-card>
    </div>
</template>

<script setup>
    import RecipeCard from "./RecipeCard.vue"
    defineProps({
        recipes : Array
    })
</script>