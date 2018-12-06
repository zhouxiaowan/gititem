<template>
    <div>
        <span :value="value" :key="index" v-for="(item,index) in max" :class="classes[index]" @click="clickStar(index)"></span>
    </div>
</template>
<script>
const clson = "star-on";
const clsoff = "star-off";
export default {
    data(){
        return {
            max:5,
        }
    },
    props:['value','disabled'],
    watch:{
        value(val){
            this.number = val;
        }
    },
    computed:{
        classes(){
            let result = [];
            for(let i = 0;i<this.value;i++){
                result.push(clson)
            }
            while(result.length<5){
                result.push(clsoff)
            }
            return result;
        }
    },
    methods:{
        clickStar(index){
            if(!this.disabled){
                this.number = index + 1;
                this.$emit('input',this.number)
            }
        }
    }
}
</script>
<style>
.star-off{
  width: 0;
  height: 0;
  margin: 6px 0;
  position: relative;
  display: block;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 7px solid #c0c4cc;
  transform:rotate(35deg);
  float: left;
  margin-right: 5px;
  cursor: pointer;
}
.star-off:before{
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 7px solid #c0c4cc;
  position: absolute;
  top: -1px;
  left: -10px;
  display: block;
  content: "";
  transform:rotate(75deg);
}
.star-off:after{
  width: 0;
  height: 0;
  display: block;
  position: absolute;
  top: 0px;
  left: -10px;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 7px solid #c0c4cc;
  content: "";
  transform:rotate(-70deg);
}
.star-on{
  width: 0;
  height: 0;
  margin: 6px 0;
  position: relative;
  display: block;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 7px solid #00c1de;
  transform:rotate(35deg);
  float: left;
  margin-right: 5px;
  cursor: pointer;
}
.star-on:before{
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 7px solid #00c1de;
  position: absolute;
  top: -1px;
  left: -10px;
  display: block;
  content: "";
  transform:rotate(75deg);
}
.star-on:after{
  width: 0;
  height: 0;
  display: block;
  position: absolute;
  top: 0px;
  left: -10px;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 7px solid #00c1de;
  content: "";
  transform:rotate(-70deg);
}
</style>
