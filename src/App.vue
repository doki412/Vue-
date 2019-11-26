<template>
  <div>
    <div id="wrapper">
        <p>第{{n+1}}手</p>
        <div class="row">
          <Cell :n="n" :winner="winner" @click="onClickCell(0,$event)" />
          <Cell :n="n" :winner="winner" @click="onClickCell(1,$event)" />
          <Cell :n="n" :winner="winner" @click="onClickCell(2,$event)" />
        </div>
        <div class="row">
          <Cell :n="n" :winner="winner" @click="onClickCell(3,$event)" />
          <Cell :n="n" :winner="winner" @click="onClickCell(4,$event)" />
          <Cell :n="n" :winner="winner" @click="onClickCell(5,$event)" />
        </div>
        <div class="row">
          <Cell :n="n" :winner="winner" @click="onClickCell(6,$event)" />
          <Cell :n="n" :winner="winner" @click="onClickCell(7,$event)" />
          <Cell :n="n" :winner="winner" @click="onClickCell(8,$event)" />
        </div>
        <div :class="{'win': isProduce}">{{winnerIs}}!</div>
    </div>
  </div>


</template>

<script>
  import Cell from './components/Cell'

  export default {
    name: 'App',
    data() {
      return {
        n: 0,
        map:[
          [null, null, null],
          [null, null, null],
          [null, null, null]
        ],
        winner: null,
      }
    },
    methods: {
      onClickCell(i, text) {
        this.n += 1;
        console.log(`${i}号被点击，内容是${text}`);
        this.map[Math.floor(i/3)][i%3] = text; 
        this.winner = this.tell(text);
      },
      tell(text){
        let result = null;
        for(let i=0; i<3; i++){
          if(this.map[i][0] !== null && this.map[i][0] ===this.map[i][1] && this.map[i][1] === this.map[i][2]){
            result = text;
            break; 
          }
        };
        for(let j = 0; j<3; j++){
          if(this.map[0][j]!==null && this.map[1][j]===this.map[0][j] && this.map[1][j]===this.map[2][j]){
            result = text;
            break;
          }
        };
        if(this.map[0][0]!==null && this.map[1][1]===this.map[0][0] && this.map[2][2]===this.map[1][1]){
            result = text;
        };
        if(this.map[0][2]!==null && this.map[0][2]===this.map[1][1] && this.map[1][1]===this.map[2][0]){
            result = text;
        }
        return result
      }
    },
    computed: {
      winnerIs(){
        if(this.winner){
          alert('YOU WIN')
          return `赢家是------${this.winner}`
        }else{
          return `胜负未分！！`
        }
      },
      isProduce:function(){
        if(this.winner){
          return true
        }else{
          return false
        }
      }
    },
    components: {
      Cell
    }
  }
</script>

<style>
  *{
    background: #D0E8EA ;
  }
  #wrapper{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center; 
  }
  .row {
    display: flex;
  }
  .win{
    color: #EC5513;
  }
</style>