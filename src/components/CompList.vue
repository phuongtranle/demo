<template>

    <div class="list-img" >
        <comp-image
            v-for="image in images"
            v-bind:key="image.id"
            v-bind:image="image"
            @ClickImage="ClickImage"
        />
    </div>


</template>
<script>
import CompImage from './CompImage';
export default {
    name:'list-user',
    props: {
        images: {
            type: Array,
            default: []
        }
    },
    components: {
        CompImage,

    },
    data() {
        return {
            loading: false,
            nextItem: 1,
        }
    },
    // mounted () {

    // // Detect when scrolled to bottom.
    //     const listElm = document.querySelector('#load-img');
    //     listElm.addEventListener('scroll', this.handleScroll)
    //     // if(listElm.scrollTop + listElm.clientHeight >= listElm.scrollHeight) {
    //     //     // this.loadMore();
    //     //     console.log('1111')
    //     // }
    //     // });

    //     // Initially load some items.
    // // console.log(listElm.scrollTop + listElm.clientHeight+'---'+listElm.scrollHeight)

    // },

    methods: {

        ClickImage(imgID){
            this.$emit('ClickImgEvent',imgID)
        }
    }

}
</script>
<style>
    .list-img {
        display: flex;
        flex-wrap: wrap;
        width: 100%;
        justify-content: space-between;
    }
</style>
