<template >
    <div class="conteiner flex flex-wrap w-full relative">
        <div class="sub_conteiner absolute w-full" v-for="(color,index) in slider" :key="index" style="overflow: hidden;">
            <transition name="fade">
                <div v-if="currentSlide == index" :class="color" style="height: 350px;"></div>           
            </transition>
        </div>
    <div class="w-full" style="height:350px">
        <div class="buttons absolute bottom-4 w-full flex justify-center">
            <div  class="button w-8 h-8 cursor-pointer rounded-full mx-2" @click="makeActive(index)" v-for="(slide, index) in slider" :key="index"
            :class="currentSlide === index ?'bg-gray-900':'bg-gray-300'"></div>
        </div>
    </div>
    </div>
    
</template>
<script>
export default {
    data() {
        return {
            currentSlide : 0,
            slider:['bg-1','bg-2','bg-3'],
            interval : '',
            isTitleShowing : true,
        }
    },
    methods: {
        makeActive(index){
            this.currentSlide = index
        }
    },
    mounted() {
       this.interval = setInterval(() => {
           this.currentSlide === 2 ? this.currentSlide = 0 : this.currentSlide++;
        }, 4000);
    },
    unmounted() {
        clearInterval(this.interval)
    },
}
</script>
<style >
.conteiner{
    display: flex;
    flex-wrap: wrap;
    position: relative;
    margin: 0;
}
.sub_conteiner{
    position: absolute;
    width: 100%;
}
.buttons{
    position: absolute;
    display: flex;
    justify-content: center;
    bottom:10%;
}
.button{
 margin: 0 .4em;
 width: 2em;
 height: 2em;
 border-radius: 100%;
 cursor: pointer;
}
.w-full{
    width: 100%;
}
.bg-1{
   background-image: url(https://upload.wikimedia.org/wikipedia/commons/9/94/Ferrari_458_Italia.JPG);
   background-position-y: center;
}
.bg-2{
   background-image: url(https://upload.wikimedia.org/wikipedia/commons/thumb/7/78/Lamborghini_Huracan_Evo_Genf_2019_1Y7A5452.jpg/1280px-Lamborghini_Huracan_Evo_Genf_2019_1Y7A5452.jpg);
    background-position-y: center;
}
.bg-3{
   background-image: url(https://upload.wikimedia.org/wikipedia/commons/6/62/Volvo_850_sedan.jpg);
   background-position-y: center;
}



.fade-enter-active, .fade-leave-active {
    transition: all 1s ease;
   
}
.fade-enter-from{
    opacity: 0;
    transform: translateX(-100%);
}
.fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
    opacity: .7;
    transform: translateX(100%);
}
</style>
