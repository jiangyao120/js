<template>
    <ul class="clearfix">
        <li @click="getphotodetail(index)" class="photo" v-for="(photo, index) in $store.state.photoList" :key="photo.src">
            <img :src="photo.src" alt="">
        </li>
    </ul>
</template>


<script>
import axios from 'axios';
export default {
    data(){
        return{
            
        }
    },
    created(){ 
        this.$emit('select', 'photo');
        axios.get('/data/photodata.json').then(res=>{
            this.$store.commit('setPhotoList',res.data.photoData);
        })
    },
    methods:{
        getphotodetail(index){
            this.$router.push(`/Photodetail/${index}`)
        }
    }
}
</script>

<style lang="scss" scoped>
.photo{
    float: left;
    width: 50%;
}
.clearfix::after{
    content: '';
    display: block;
    clear: both;
}


</style>

