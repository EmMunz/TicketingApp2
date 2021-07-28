<template>
<div>
  <h1>This is our first page</h1>
  <component :is="DynamicCards"/>
</div>
</template>
<script>
//For the component page to show in this index page, we have to import it just right below this
import DynamicCards from "~/components/DynamicCards.vue";
export default {
  component:{
    DynamicCards
  },
  data(){
    return{
       DynamicCards
    }
  }
}
</script>