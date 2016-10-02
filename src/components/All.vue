<template>
  <div class="parent">
    <h1 class="children">{{ msg }}</h1>
  </div>
</template>

<script>
export default {
  data () {
    return {
      msg: 'Happy birthday!'
    }
  }
}
</script>
<style scoped>
h1 {
  color: yellow;
}
.parent {
  display:flex;
  align-items: center;/*垂直居中*/
  justify-content: center;/*水平居中*/
  width:100%;
  height:100%;
  min-height:500px;
}
.children {
}
</style>
