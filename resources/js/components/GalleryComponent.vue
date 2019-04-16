<template>
    <div>
        <ul class="">
            <li v-for="img in photos.slice(0, limit)" style="">
                <a href="#0"><img :src="img.thumbnailUrl">
                    <div class="box_data">
                        <span></span>
                    </div>
                </a>
            </li>
        </ul>
        <button class="btn btn-primary" @click="showMore">Show More</button>
    </div>
</template>

<script>
export default {
    name: 'Gallery',
    data(){
        return{
            photos:{},
            limit: 5,
        }
    },
    methods:{
        showMore(){
            this.limit += 5; 
        }
    },
    mounted(){
        axios.get('https://jsonplaceholder.typicode.com/photos')
        .then((response) => this.photos = response.data)
        .catch((errors) => console.log(errors))
    },
    created(){

    },
}
</script>

<style scoped>
img{ max-width:100%;}

.gallery_box li{ width:33.333333%; max-width: 100% ; display:inline-block; float: left; text-align: center; overflow: hidden;    position: relative; height: 300px;}
.gallery_box{ padding:0;display: flow-root;}

.gallery_box li:hover img {
    -moz-transform: scale(1.1);
    -webkit-transform: scale(1.1);
    -ms-transform: scale(1.1);
    -o-transform: scale(1.1);
    transform: scale(1.1);
}
.gallery_box li img{-webkit-transition: transform 0.5s ease;
    -o-transition: transform 0.5s ease;
    transition: transform 0.5s ease;}
.gallery_box li:nth-child(even) {
    height: 304px;
}
.gallery_box li:nth-child(odd) {
    height: 438px; 
}
.gallery_box li:nth-child(odd) .box_data{ background:rgba(0,0,0,0.17) }
.gallery_box li:nth-child(even) .box_data{ background:rgba(0,44,255,0.27) }
.gallery_box .box_data{ position:absolute; top: 0; left: 0; right:0; bottom:0; color:#fff;}
.gallery_box .box_data span{ position:absolute; top: 50%; transform: translateY(-50%); left:0 ; right:0; font-size:24px;}
.gallery_box li:hover .box_data{ background:rgba(255,0,39,0.55)}
</style>
