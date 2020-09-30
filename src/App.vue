<template>
  <div id="app">
    <FormReserva @enviarData="this.dataReserva" />
    <TimeLine :reservas='reservas' />
    <TablaReserva :reservas='reservas' :borrarReserva='borrarReserva'/>
  </div>
</template>

<script>
import TablaReserva from './components/TablaReserva.vue'
import TimeLine from './components/TimeLine'
import FormReserva from './components/FormReserva'

export default {

  components: { FormReserva, TimeLine, TablaReserva },
  name: 'App',

   data() {
    return {
      reservas: [],
    };
   },

  methods: {
   dataReserva( e ){
     if(e.name != "" && e.date != "" && e.timeStart != "" && e.timeEnd != "" ){
     const infoReserva={
       "id": this.reservas.length,
        "content": e.name,
        "start": `${e.date} ${e.timeStart}`,
        "end":   `${e.date} ${e.timeEnd}`,
        }
     this.reservas.push({...infoReserva})}else{
       alert('completa los todos campos')
     }
   },
   borrarReserva(res){
     let ver = this.reservas.indexOf(res)
    //  console.log(ver)
     this.reservas.splice(ver,1)
   
   }
  },

}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
