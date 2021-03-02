<template>
  <div id="app">
    <h1 class="text-center">Historias</h1>
    <Historia :historia="this.$data.alex"></Historia>
    <hr>
    <Historia :historia="this.$data.juan"></Historia>
    <hr>
    <div class="row">
      <div class="col col-6 p-4">
        <input type="text" class="form-control" v-model='filtro' placeholder="Buscar...">
      </div>
    </div>
    <div class="alert alert-danger" role="alert" v-bind:key="item.historia" v-for="item in mostrarFiltro">
      <b>{{item.nombre}} dice: </b>"{{item.historia}}"
    </div>
    <p ></p>
  </div>
</template>

<script>
import Historia from './components/Historia';
import EventBus from './bus'

export default {
  name: 'App',
  components: {Historia},
  computed: {
    mostrarFiltro(){
      let historiasJuntas = this.juan;
      let juntar = historiasJuntas.concat(this.alex) 
      return juntar.filter(item => item.historia.includes(this.filtro));
    },
  },
  
  data(){return{
    filtro: '',
    juan: [ {nombre: 'Juan', historia: 'hola juan'},
            {nombre: 'Juan', historia: 'Esta es una nueva historia de juan'},
    ],
    alex: [ {nombre: 'Alex', historia: 'Esta es una historia de alex'},
            {nombre: 'Alex', historia: 'Nueva historia de alex.'},
    ],
    Juntar: [],

  }},
  created: function(){
    EventBus.$on('add-historia', (data) =>{
      if (data[1] == 'Alex') {
        this.alex.push({nombre: data[1], historia: data[0]});
      }else{
        this.juan.push({nombre: data[1], historia: data[0]});
      }
    })
  }
}
</script>

<style>

</style>
