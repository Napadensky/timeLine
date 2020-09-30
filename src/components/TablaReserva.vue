<template>
  <div class="container">
    <table class="tabla-reservas">
      <tr>
        <th class="th-left">Nombre</th>
        <th class="col-hours">Horario</th>
        <th class="col-acction">Accion</th>
      </tr>

      <tr v-for="(res, index) in reservas" :key="index">
        <td class="th-left">{{ res.content }}</td>
        <td class="col-hours">
          de {{ res.start.slice(10, 16) }} a {{ res.end.slice(10, 16) }}
        </td>
        <td class="col-acction">
          <button class="btn-del" @click="borrarReserva(res)">
            <i class="large material-icons">delete</i>
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "TablaReserva",
  props: ["reservas", "borrarReserva"],
};
</script>

<style lang="scss" scoped>
.tabla-reservas {
  margin: auto;
  width: 80%;
  .col-hours {
    text-align: right;
  }
  .col-acction {
    max-width: auto;
    display: inline-block;
  }
  .th-left {
    text-align: left;
  }
  .btn-del{
    padding: 0px 30px;
    background-color: #ffffff;
    color:rgb(134, 134, 134);
    border: none;
    
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px 0px;
    cursor: pointer;
    border-radius: 4px;
    height: 30px;
  }
}
</style>