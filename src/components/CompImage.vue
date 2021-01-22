<template>
    <div class="image">
        <!-- <pre>{{image}}</pre> -->
        <!-- <img :src="image.images.original.url" > -->
        <picture>
            <source :srcset="image.images.fixed_height_still.url" media="(max-width: 420px)">
            <source :srcset="image.images.preview.url" media="(max-width: 840px)">
            <img :src="image.images.original.url"
                @click="ClickImg()"
            >
        </picture>
        <p>{{image.id}}</p>
        <div class="popup" v-if="active">
            <img :src="image.images.original.url" >
            <a class="close" @click="close()">X</a>
        </div>
    </div>
</template>
<script>
export default {
    name:'comp-image',
    props: {
        image: {
            type: Object,
            default: null
        }
    },
    data() {
        return {
            active:false
        }
    },
    mounted(){

    },
    methods: {

        ClickImg(){

            this.active = !this.active;
            var imgID = {
                id: this.image.id
            }
            this.$emit('ClickImage', imgID);
            this.setBodyClass()
        },
        close(){
            this.active = !this.active;
            this.rmBodyClass()
        },
        setBodyClass(){
            let body = document.body
            body.classList.add('noscroll')
        },
        rmBodyClass(){
            let body = document.body
            body.classList.remove('noscroll');
        }

    }
}
</script>
<style>
    .image {
        width: 24%;
    }
    .image img {
        height: 40vh;
        width: 100%;
        object-fit: cover;
        cursor: pointer;
    }
    .popup {
        position: absolute;
        width: 80%;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        background-color: #fff;
        padding: 20px;
        height: 90%;
    }
    .popup img {
        height: 90vh;
        object-fit: cover;
    }
    .noscroll {
        overflow: hidden;
    }
    .popup .close {
        font-size: 20px;
        color: #fff;
        background-color: #ccc;
        padding: 10px 20px;
        position: absolute;
        top: 0;
        right: 0;
        font-weight: bold;
        cursor: pointer;
    }
    @media (min-width: 421px) and (max-width: 840px) {
        .image {
            width: 32%;
        }
    }
    @media (min-width: 300px) and (max-width: 420px) {
        .image {
            width: 49%;
        }
    }
</style>
