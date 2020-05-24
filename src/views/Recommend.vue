<template>
    <div class="recommend">
        <!--my-swiper  -->
      <my-swiper
      :swiper-list="swiperList"
      :swiper-option="swiperOption"
      />
      <!-- song-sheet-list -->
      <song-sheet-list
        :hot-song="hotSong"
      />
    </div>
</template>
<script>
import MySwiper from '@/components/main/recommend/MySwiper'
import SongSheetList from '@/components/main/recommend/SongSheetList'
export default {
    data(){
        return {
            swiperList: [],

            swiperOption: {
             pagination: {
              el: '.swiper-pagination'
           },
          // Some Swiper option/callback...
          loop:true,
          autoplay:true//自动轮播
         },
       hotSong:[]
       }
    },
    methods:{
          async fetchSwiperList(){
              const res=await this.$http.get('/banner');
              console.log(res.data);
              this.SwiperList=res.data.data.map(item=>({img:item.pic_info.url}))
          
          },
           //获取歌单列表数据（热门歌曲）
        async fetchHotSong() {
            const res = await this.$http.get('/recommend/playlist');
            this.hotSong = res.data.data.list.map(item => ({
                id: item.tid,
                img: item.cover_url_small,
                title: item.title,
                info: item.creator_info.nick
            }))
        }
    },
    created(){
        //   this.fetchSwiperList();
          this.fetchHotSong();
    },
    components:{ 
         MySwiper,
         SongSheetList
         }
      

}
</script>