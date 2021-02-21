<!-- <template>
  <div class="hello">
    <ul class="text-center ">
    <select v-model="selected">
          <option v-for="item in info" :key="item.id" :value=item.year>{{item.year}}</option>
      </select>
    </ul>
    <button @click.prevent="applychanges(selected)">Actualizar</button>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  emits: ["panel"],
    setup(_,{emit}) {
        function panel() {
            emit("panel");
        }

        return {panel}
    },
 data() {
   return {
     info : {},
     
   }
 },
  mounted() {
    
 },
  methods: {
   
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style> -->
