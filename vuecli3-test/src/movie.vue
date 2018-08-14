<template>
    <div>
        <ul>
        <li class="movie" v-for="movie in movieList" :key="movie.id">
            <div class="movie-img">
                <img :src="movie.images.large" alt="">
            </div>
            <div class="movie-info"> 
                <div class="movie-info-title">{{movie.title}}</div>
                <div class="movie-info-art">观众评语：{{movie.rating.average}}</div>
                <div class="movie-info-star">演员：
                    <span v-for="star in movie.casts" :key="star.id">{{star.name}}</span>
                </div>
            </div>
        </li>
    </ul>
    <div>
        <div class="end" v-show="isEnd">到底了老铁</div>
        <div class="loading" v-show="isLoading">
            <img src="@/assets/img/loading.gif" alt="">
        </div>
    </div>
    </div>
    

</template>


<script>
import axios from "axios";
export default {
  data() {
    return {
      movieList: [],
      isLoading: true,
      isEnd: false
    };
  },
  methods: {
    getData() {
      
      let url2 = "https://api.myjson.com/bins/pb8vw";
      this.isLoading = true;
      axios.get(url2).then(res => {
        
        let getList = res.data.subjects.slice(
          this.movieList.length,
          this.movieList.length + 5
        );
        if (getList.length < 5) {
          this.isEnd = true;
        }
        this.movieList = this.movieList.concat(getList);
        this.isLoading = false;
      });
    }
  },
  created() {
    this.$emit("select", "movie");
    this.getData();
  },
  mounted() {
    window.onscroll = () => {
      let scrollTop = document.documentElement.scrollTop;
      let scrollHeight = document.documentElement.scrollHeight;
      let clientHeight = document.documentElement.clientHeight;
      console.log(scrollHeight, scrollTop, clientHeight);
      if (scrollHeight == scrollTop + clientHeight && !this.isEnd) {
        // 请求数据
        this.getData();
      }
    };
  }
};
</script>

<style lang="scss" scoped>
        .movie{
            display: flex;
            padding: 0.2rem;
            border-bottom: 0.02rem soild #ccc;
            &-img{
                flex-grow: 1;
                width: 0;
            }
            &-info{
                flex-grow: 4;
                width: 0;
                margin-left: 0.2rem;
                &-tatle{
                    font-weight: 700;
                    color: black;
                    font-size: 0.35rem;
                }
                &-art{
                    font-weight: 700;
                    color: #faaf00;
                }
                &-star{
                    color: #666;
                    font-size: 0.26rem;
                }

            }
        }
        
        .loading{
            position: fixed;
            bottom: 0;
            width: 100%;
            text-align: center;
            img{
                width: 3rem;
            }
        }
</style>

