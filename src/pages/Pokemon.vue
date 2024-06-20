<template>
  <h1>hello from PokemonPage</h1>
<pokemon-image />
<pokemon-options/>
</template>

<script>
import PokemonImage from '@/components/PokemonImage.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
export default {
    components:{
        PokemonImage,
        PokemonOptions,
    }

}
</script>

<style>

</style>