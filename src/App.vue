<template>
<div class="wrap">
    <div class="control">
       <div>第{{n}}手</div>
       <div>
         <button @click="reset">
           重新开始
         </button>
       </div>
    </div>
    <div class="chess">
    <div class="row">
    <Cell @click="onCellClick(0,$event)" v-bind:n="n" :isfinish="isfinish" />
    <Cell  @click="onCellClick(1,$event)"  v-bind:n="n" :isfinish="isfinish"/>
    <Cell  @click="onCellClick(2,$event)" v-bind:n="n" :isfinish="isfinish"/>
    
  </div>
   <div class="row">
    <Cell  @click="onCellClick(3,$event)" v-bind:n="n" :isfinish="isfinish"/>
    <Cell  @click="onCellClick(4,$event)" v-bind:n="n" :isfinish="isfinish"/>
    <Cell  @click="onCellClick(5,$event)" v-bind:n="n" :isfinish="isfinish"/>

  
  </div>
   <div class="row">
   <Cell  @click="onCellClick(6,$event)" v-bind:n="n" :isfinish="isfinish"/>
    <Cell  @click="onCellClick(7,$event)" v-bind:n="n" :isfinish="isfinish"/>
    <Cell  @click="onCellClick(8,$event)" v-bind:n="n" :isfinish="isfinish"/>
  </div>
  <div class="footer">
    <span v-if="isfinish">{{result}}胜利</span>
    <div v-if="even">{{even}}</div>
  </div>
 </div>
</div>
</template>

<script>
import Cell from "./components/Cell";
export default {
  data(){
    return {
      n:0,
      isfinish:false,
      map:[   //二维数组存“x”或者“y”
        [null,null,null],
        [null,null,null],
        [null,null,null],  
      ],
      result:null,
      even:false
    }
  },
  components: {
    Cell
  },
  methods:{
    onCellClick(i,text){
      console.log(`${i}值${text}`)
      this.map[Math.floor(i/3)][i%3]=text;
      this.n=this.n+1
      this.tell()
    },
    tell(){
     const {map,text}=this
     for(let i=0;i<2;i++){
       if(map[i][0]!=null&&map[i][0]==map[i][1]&&map[i][1]==map[i][2]){
         this.result=map[i][0];
         this.isfinish=true
       }
     }
     for(let j=0;j<2;j++){
       if(map[0][j]!=null&&map[0][j]==map[1][j]&&map[1][j]==map[2][j]){
         this.result=map[0][j];
         this.isfinish=true

       }
     }
     if(map[0][0]!=null&&map[0][0]==map[1][1]&&map[1][1]==map[2][2]){
         this.result=map[0][0];
         this.isfinish=true

     }
     if(map[2][0]!=null&&map[2][0]==map[1][1]&&map[1][1]==map[0][2]){
         this.result=map[2][0];
         this.isfinish=true

     }
      if (map.flat(2).every(item => item !== null) && !this.isfinish) {
        this.even = "平局";
      }
    },
    reset(){
      console.log(this.$children)
      this.$children.map(item => {
        item.status = false;
        item.text = null;
      });
      this.map = [
        [null, null, null],
        [null, null, null],
        [null, null, null]
      ];
      this.result = null;
      this.n = 0;
      this.isfinish = false;
    }
  }
};
</script>
<style>
.row{
  display: flex;
}
.wrap{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.control{
  display: flex;
  justify-content:space-between;
  align-items: center;
  width: 310px;
  margin-bottom: 5px;
}
.footer{
  text-align: center;
  font-size: 25px;
}
</style>
