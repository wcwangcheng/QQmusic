<template>
    <div class="Seach">
       <input type="text" placeholder="请输入你想搜索的歌名" style="width:65%;height:25px; margin-left:15%; color:green; border-radius:5px;">
      
      
 <!-- 热门搜索列表 -->
 <div>
    <h3>大家都在搜</h3>
       <ul class="pt-3 px-4">
        <li 
        class="d-flex pb-3"
        v-for="item of  SeachList"
        :key="item.name"
        >
       <ol>
           <li>{{item.name}} <a style="font-size:5px;position:absolute;right:0px">{{item.logo}}</a> </li>
        
       </ol>
        </li>
    </ul>
 </div>
   
      
          
            

    </div>
</template>

<script>

export default {
    data() {
        return {
            SeachList: []
        }
    },
   
    methods: {
       //获取热门搜索列表
        async fetchSeachList() {
           
            const res = await this.$http.get('/search/hot')
            this.SeachList = res.data.data.map(item=>({
                name:item.k,
                logo:item.n
            }))
            console.log(this.SeachList);
            
        }
    }, 
    created() {
        this.fetchSeachList()
    },
    components: {
       
    }
}
</script>