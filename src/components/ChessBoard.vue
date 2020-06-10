<template>
  <div class='board'>
    <div class='board-row'>
      <ChessSquare 
        v-for='(state,index) in chessState[0]'
        :key='`${state}row0col${index}`'
        :state='state'
        :row='0'
        :col='index'
        @put-piece='$emit("put-piece",$event)'
      />
    </div>
    <div class='board-row'>
      <ChessSquare 
        v-for='(state,index) in chessState[1]'
        :key='`${state}row1col${index}`'
        :state='state'
        :row='1'
        :col='index'
        @put-piece='$emit("put-piece",$event)'
      />
    </div>
    <div class='board-row'>
      <ChessSquare 
        v-for='(state,index) in chessState[2]'
        :key='`${state}row2col${index}`'
        :state='state'
        :row='2'
        :col='index'
        @put-piece='$emit("put-piece",$event)'
      />
    </div>
  </div>
</template>

<script>
import ChessSquare from './ChessSquare.vue'
export default {
  name: 'ChessBoard',
  components: {
    ChessSquare
  },
  props: {
    chessState: Array
  }
}
</script>

<style scoped>
.board{
  display: inline-block;
  border: 1px solid black;
  width: fit-content;
  vertical-align: top;
  margin-right: 10px;
}
.board-row{
  display: flex;
  width: fit-content;
}
</style>
