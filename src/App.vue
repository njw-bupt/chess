<template>
  <div class='chess-app'>
    <h1>Funny Chess</h1>
    <div class='chess-app-content'> 
      <ChessBoard 
        :chess-state='chessState' 
        @put-piece='putPiece'
      />
      <OperateBoard 
        :result='result'
        @restart-game='restartGame'
      />
    </div>
  </div>
</template>

<script>
import ChessBoard from './components/ChessBoard.vue'
import OperateBoard from './components/OperateBoard.vue'

export default {
  name: 'App',
  components: {
    ChessBoard,
    OperateBoard
  },
  data(){
    return {
      chessState: [
        ['','',''],
        ['','',''],
        ['','','']
      ],
      stepCount: 0, //偶数O，基数X
      result: ''
    }
  },
  methods: {
    putPiece: function(location){
      let row = location.row,
          col = location.col;
      //判断是否可以在该位置落子
      if(this.chessState[row][col]=='' && !this.result){
        //判断哪方落子
        let curPiece = this.stepCount%2==0? 'O' : 'X';

        //this.chessState[row][col] = curPiece; //vue不能检测数组和对象的变化
        let newChessState = [[],[],[]];
        for(let i=0; i<this.chessState.length; i++){
          for(let j=0; j<this.chessState[0].length; j++){
            newChessState[i][j] = this.chessState[i][j];
          }
        }
        newChessState[row][col] = curPiece;
        this.chessState = newChessState;

        this.stepCount++;
      }
    },
    judgeRes: function(){
      //判断是否出现获胜情况
      //横排
      for(let i=0; i<this.chessState.length; i++){
        let row = this.chessState[i];
        let curPiece = row[0];
        if(curPiece){
          let curRes = true;
          for(let j=1; j<row.length; j++){
            curRes = curRes && (curPiece == row[j]);
          }
          if(curRes){
            return curPiece;
          }
        }
      }
      //竖排
      for(let i=0; i<this.chessState.length; i++){
        let curPiece = this.chessState[0][i];
        if(curPiece){
          let curRes = true;
          for(let j=1; j<this.chessState[0].length; j++){
            curRes = curRes && (curPiece == this.chessState[j][i]);
          }
          if(curRes){
            return curPiece;
          }
        }
      }
      //斜排
      //左上至右下
      let curPieceLeftToRight = this.chessState[0][0];
      if(curPieceLeftToRight){
        let curResLeftToRight = true;
        for(let i=1; i<this.chessState.length; i++){
          curResLeftToRight = curResLeftToRight && (curPieceLeftToRight == this.chessState[i][i]);
        }
        if(curResLeftToRight){
          return curPieceLeftToRight;
        }
      }
      //右上至左下
      let curPieceRightToLeft = this.chessState[0][2];
      if(curPieceRightToLeft){
        let curResRightToLeft = true;
        for(let i=1,j=1; i<this.chessState.length; i++,j--){
          curResRightToLeft = curResRightToLeft && (curPieceRightToLeft == this.chessState[i][j]);
        }
        if(curResRightToLeft){
          return curPieceRightToLeft;
        }
      }

      //判断是否平局
      let hasResult = true
      for(let i=0; i<this.chessState.length; i++){
        for(let j=0; j<this.chessState[0].length; j++){
          hasResult = this.chessState[i][j] && hasResult;
        }
      }
      if(hasResult){
        return 'none'; 
      }

      return ''; 
    },
    restartGame: function(){
      this.chessState = [
        ['','',''],
        ['','',''],
        ['','','']
      ];
      this.stepCount = 0;
      this.result = '';
    }
  },
  updated(){
    let res = this.judgeRes(); //未出结果的返回值'',平局返回值'none',获胜返回值'O'/'X'
    if(res){
      this.result = res;
    }
  }
}
</script>

<style>
.chess-app{
  margin-left: auto;
  margin-right: auto;
  /* text-align: left; */
  width: fit-content;
  
}
.chess-app .chess-app-content{
  
}
</style>
