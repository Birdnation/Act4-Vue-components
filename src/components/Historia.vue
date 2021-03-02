<template>
    <div>
        <h4>Historias de {{historia[0].nombre}}</h4>
        <div class="row">
            <div class="col col-6 p-3"><input type="text" class="form-control" v-model="history" v-on:keyup.enter="addHistoria" placeholder="Agregar nueva historia..."></div>
        </div>

        <div  v-bind:key="data.historia" v-for="data of historia" class="alert alert-primary" role="alert">
            <b>{{historia[0].nombre}} dice: </b> "{{data.historia}}"
        </div>
    </div>
</template>

<script>
import EventBus from '../bus'
export default {
    name: 'Historia',
    props:['historia'],
    data(){
        return{
            history: ''
        }
    },
    methods:{
        addHistoria: function(){
            EventBus.$emit('add-historia', [this.history, this.historia[0].nombre]);
            this.history = '';
        }
    }
}
</script>