<template>    
  <div class="headPoke">    
    <h1>{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Tittle',
  // This props is comming since parent component not in states
  props: {
    msg: String
  }
}
</script>


