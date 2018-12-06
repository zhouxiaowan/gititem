<template>
    <li :class="menuetype?'open':''" @click.stop="menueOpen()">
        <a href='javascript:void(0)' :level="item.level">
            <i v-if="item.list" class="ico-triangle"></i>
            <span>{{item.text}}</span>
        </a>
        <ul v-show="menuetype">
            <sliderbar :item="obj" :key="key" v-for="(obj,key) in item.list"></sliderbar>
        </ul>
    </li>
</template>
<script>
import sliderbar from '@/components/sliderbar';
export default {
    name:"sliderbar",
    components:{
        sliderbar
    },
    props:['item'],
    data(){
        return {
            menuetype:false
        }
    },
    methods:{
        menueOpen(){
            this.menuetype = !this.menuetype;
        }
    }
}
</script>
<style>
*{
    list-style: none;
    padding: 0;
    margin: 0;
    text-decoration: none;
    color:#373d41;
}
.open>a>.ico-triangle{
    border-color: #333 transparent transparent transparent;
}
.ico-triangle{
    display: inline-block;
    width:0;
    height: 0;
    border-width: 5px;
    border-style:solid;
    border-color: transparent transparent transparent #333;
}
a[level='2']{
    margin-left: 30px;
}
a[level='3']{
    margin-left: 60px;
}
a[level='4']{
    margin-left: 90px;
}
</style>
