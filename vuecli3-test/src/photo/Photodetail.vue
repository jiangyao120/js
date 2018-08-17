<template>
<router-link to="/Photo">
     <v-touch @swipeleft="swipeleft" @swiperight="swiperight" class="img" :style="{background: 'url('+imgsrc+') no-repeat center/contain #000'}"></v-touch>
</router-link>
   
</template>
<script>
export default {
    data(){
        return{
            imgsrc:'',
            nowindex:-1,
        }
    },
    watch:{
        nowindex(){
            let nowimg = this.$store.state.photoList[this.nowindex];
            if(nowimg){
                this.imgsrc=nowimg.src;
            }
        }

    },
    methods:{
            swipeleft(){
                this.nowindex--;
                if(this.nowindex==-1){
                    this.nowindex=this.$store.state.photoList.length -1;
                }
            },
            swiperight(){
                this.nowindex++;
                if(this.nowindex==this.$store.state.photoList.length){
                    this.nowindex=0;
                }
            },

    },
    created(){
        this.nowindex=this.$route.params.ind;
        
    },
}
</script>
<style lang="scss" scoped>
.img{
    position: absolute;
    top: 1rem;
    left: 0;
    right: 0;
    bottom: 1rem;

}
</style>
