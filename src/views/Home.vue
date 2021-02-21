<template>
  <div class="home">
   <slider/>
   <div class="w-full h-28 bg-blue-700 mt-1">
      <div class="absolute text-center text-white w-full">
        <h3 class="text-4xl my-2">AUTOS CLASICOS</h3>
        <p>Mira los mejores autos classicos</p>
      </div>
   </div>
    <div class="flex pt-4 h-auto">

        <div class="panel mx-8 w-1/5  rounded-lg  shadow-2xl">
            
            <select v-model="selected" class="w-52 border border-gray-600 rounded-lg shadow-2xl px-2 py-4 mx-2 my-4" >
                  <option v-for="item in infoAll" :key="item.id" :value=item.year>{{item.year}}</option>
              </select>
            
            <button @click.prevent="applychanges(selected)" class="my-2 block mx-8 bg-blue-700 text-white rounded-sm p-2 hover:opacity-75">Actualizar</button>
            <button v-if="panelOpen" @click="panelOpen = false" class="my-2 block mx-8 bg-red-700 text-white rounded-sm p-2 hover:opacity-75">Cancelar</button>
        </div>
        
        <div v-if="panelOpen" class="grid grid-cols-1 gap-2 sm:grid-cols-3 w-full pl-4">
          <div  v-for="item in state.panelResponse" :key="item.id" class="rounded-lg border shadow-2xl w-full cursor-pointer hover:opacity-80" @click="OpenModal(state.panelResponse)">
            <div class="md:h-auto">
            <img class="w-full h-48 object-cover rounded-t-lg" :src=item.img>
            <div class="">
              <h4 class="w-48 font-mono">Car name: {{item.title}}</h4>
            <code>Year : {{item.year}}</code>
            </div>
            </div>
          </div>  
        </div>
        
        <div v-else class="grid grid-cols-1 gap-2 sm:grid-cols-3 w-full pl-4">
          <div v-for="item in state.info" :key="item.id" class="rounded-lg border shadow-2xl w-full cursor-pointer hover:opacity-80" @click="OpenModal(item)">
            <div class="md:h-auto">
            <img class="w-full h-48 object-cover rounded-t-lg" :src=item.img>
            <div class="">
              <h4 class="w-48 font-mono">Car name: {{item.title}}</h4>
            <code>Year : {{item.year}}</code>
            </div>
            </div>
          </div>
        </div>

    </div>
    <div >

      <div class="flex w-full justify-center bg-blue-700">
        <div v-for="link in state.links" :key="link">
        <button @click.prevent="getElements(link.label)" :class="link['active'] ?'text-pink-700':''" class="mx-4 py-4 text-white">
        {{link.label}}
        </button>
       </div>
      </div>
  </div>
   <modal v-if="isModalOpen" @close='isModalOpen= false'>
                <template v-slot:title>
                    {{state.ModalValue.title}}
                </template>
                <template v-slot:img>
                    <img class="w-full" :src=state.ModalValue.img >
                </template>
                <template v-slot:body>
                    {{state.ModalValue.body}}
                </template>
                <template v-slot:year>
                    {{state.ModalValue.year}}
                </template>
            </modal>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import slider from '@/components/slider.vue'
import modal from '@/components/modal.vue'
import {ref,reactive,onMounted} from 'vue'
import axios from 'axios';
export default {
  name: 'Home',
  components: {
    // HelloWorld,
    slider,
    modal,
  },
  setup(){
        const isModalOpen = ref (false);
        const  panelOpen = ref (false);
        const state = reactive({
          ModalValue :{},
          panelResponse:null,
          page:1,
          info:null,
          links:null,
        });

        function getElements(page){
          axios.get('http://localhost:8000/api/articles?page='+ page)
          .then(response => {
            state.info = response.data.data;
            state.links = response.data.meta.links;
            console.log(state.links);
            })
    }
        onMounted(() => {
          getElements(state.page);
        })



        function applychanges(selected){
        axios.get('http://localhost:8000/api/articles/year/'+selected)
        .then(response => {state.panelResponse = response.data;
        panelOpen.value = true ;})  
    }
        function OpenModal(item){
          state.ModalValue = item;
          isModalOpen.value = true;
        }
       
        return {isModalOpen,OpenModal,state,applychanges,panelOpen,getElements}
  },
  data() {
    return {
      
      infoAll:null,
      
      
      selected:'',
    }
  },
  mounted() {
    
    this.getElementsAll();
    
  },
  methods: {
   
     getElementsAll(){
      axios.get('http://localhost:8000/api/articles/all')
      .then(response => {this.infoAll = response.data;})   
    },
    
  },
}
</script>
<style>
</style>