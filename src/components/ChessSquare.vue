<template>
  <div 
    class='square' 
    @click='$emit("put-piece", {row, col})'
  >
    <span>{{ state }}</span>
  </div>
</template>

<script>
export default {
  name: 'ChessSquare',
  props: {
    state: String,
    row: Number,
    col: Number
  },
}
</script>

<style scoped>
.square{
  border: 1px solid black;
  text-align: center;
  vertical-align: middle;
  line-height: 60px;
  font-size: 35px;
  width: 60px;
  height: 60px;
}
</style>
