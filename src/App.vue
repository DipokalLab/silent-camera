<template >

<div class="container-fluid h-full mx-auto overflow-hidden bg-black">
  

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
