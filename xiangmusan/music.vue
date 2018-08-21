<template>
    <scribble :musicList='musicList'></scribble>
</template>


<script>
import axios from 'axios';
import scribble from '@/components/Scribble.vue';
export default {
     data(){
        return {
            musicList:[],
        };
    },
    created(){ 
        
        this.$emit('select', 'music');
        axios.get('/data/musicdata.json').then(res=>{
            this.musicList = res.data.musicData;
        })
    },
    components: {
        scribble,
    }
    
}
</script>

<style lang="scss" scoped>

</style>
