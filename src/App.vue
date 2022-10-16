<template >

<div class="container h-full mx-auto ">
  

<Camera class="h-full" />
</div>
</template>

<script>
import Camera from './components/Camera.vue'
import 'material-icons/iconfont/material-icons.css';


export default {
  name: 'App',
    components: {
      Camera
  }
}
</script>
