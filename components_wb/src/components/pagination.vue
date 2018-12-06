<template>
    <div>
        <ul class="paging">
            <li>
                <input class="show-num" @click="showPageCount()" readonly="readonly" v-model="pageCount" type="text">
                <ul class="select-count" v-show="showPagecount">
                    <li :key="index" v-for="(item,index) in pagesortnum" @click="selectPageCount(item)">{{item}}</li>
                </ul>
            </li>
            <li @click="pagerClick(currentPage-1)">上一页</li>
            <li :class="currentPage==index?'pager-on':'pager-off'" :key="key" v-for="(index,key) in indexes">
                <a @click="pagerClick(index)">{{index}}</a>
            </li>
            <li @click="pagerClick(currentPage+1)">下一页</li>
            <li>共{{total}}页</li>
            <li>
                <span>前往</span>
                <input v-model.number="pagenum"  @keyup.enter="onEnter(pagenum)" type="text"/>
                <span>页</span>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    data(){
        return {
            currentPage:1,
            pagenum:1,
            pageCount:'20条/页',
            showPagecount:false,
            pagesortnum:[
                "20条/页","50条/页","100条/页","200条/页"
            ]
        }
    },
    props:['total'],
    computed:{
        indexes(){
            let arr = [];
            let left = 1;
            let right = this.total;
            if(this.total>10){
                if(this.currentPage>5&&this.currentPage<this.total-4){
                    left = this.currentPage-5;
                    right = this.currentPage+4;
                }else{
                    if(this.currentPage<=5){
                        left = 1;
                        right= 11;
                    }else{
                        left = this.total - 9;
                        right = this.total;
                    }
                }
            }
            while(left<=right){
                arr.push(left++);
            }
            return arr;
        }
    },
    methods: {
        pagerClick(index){
            this.currentPage = index;
        },
        onEnter(pagenum){
            if(pagenum>this.total){
                this.currentPage = this.total;
            }else if(pagenum<1){
                this.currentPage = 1;
            }else{
                this.currentPage = pagenum;
            }
        },
        showPageCount(){
            this.showPagecount = !this.showPagecount
        },
        selectPageCount(item){
            this.pageCount = item || this.pagesortnum[0];
            this.showPagecount = false;
        },
        autoHide(evt) {
            if (!this.$el.contains(evt.target)) {
                this.showPagecount = false;
            }
        },
    },
    mounted() {
        document.addEventListener("click", this.autoHide, false);
    },
    destroyed() {
        document.removeEventListener("click", this.autoHide, false);
    },
    watch:{
        currentPage(){
            this.pagenum = this.currentPage;
        }
    }
}
</script>
<style>
.paging li{
    float: left;
    margin-right: 15px;
    cursor: pointer;
}
.paging li>a:hover{
    color: #00c1de;
}
.pager-on a{
    color: #00c1de;
    cursor: pointer;
}
.pager-off a{
    cursor: pointer;
}
.select-count{
    overflow: hidden;
    border: 1px solid #e4e7ed;
    box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
    background-color: #ffffff;
}
.select-count li{
    float: none;
    padding: 6px 0;
    text-align: center;
}
.select-count li:hover{
    color: #00c1de;
}
.show-num{
    cursor: pointer;
}
</style>


