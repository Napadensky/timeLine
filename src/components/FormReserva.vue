<template>
  <div class="form-content container">
    <h1 class="title-reserva">RESERVAR</h1>

    <form @submit.prevent="enviarData">
      <div >
        <label for="name">Nombre</label>
        <input type="text" name="name" v-model="dataReserva.name" />
      </div>

      <div >
        <label for="date">Fecha</label>
        <input type="date" name="date" v-model="dataReserva.date" />
      </div>

      <div >
        <label for="date">Desde</label>
        <input type="time" name="tameStart" v-model="dataReserva.timeStart" />
      </div>

      <div >
        <label for="date">Hasta</label>
        <input type="time" name="timeEnd" v-model="dataReserva.timeEnd" />
      </div>

      <div>
        <button type="submit">Guardar</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {

  name: "FormReserva",
  
  data() {
    return {
      dataReserva: {
        name: "",
        date: "",
        timeStart: "",
        timeEnd: "",
      },
    };
  },

  methods: {
    enviarData() {
      // console.log(this.dataReserva)
      this.$emit("enviarData",this.dataReserva)
    },
  },

};
</script>

<style lang="scss" scoped>
.title-reserva {
  text-align: left;
  color: #04a399;
}
.form-content {
  margin: auto;
  width: 80%;
  padding: 50px;
  -webkit-box-shadow: 0px 0px 0.2px 0.2px rgba(0, 0, 0, 0.75);
  -moz-box-shadow: 0px 0px 0.2px 0.2px rgba(0, 0, 0, 0.75);
  box-shadow: 0px 0px 2.2px 0.2px rgba(0, 0, 0, 0.75);
}

form {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-wrap: wrap;
  div {
    margin: 0 10px;
    label {
      display: block;
      text-align: left;
      padding-bottom: 10px;
    }
    input {
      -webkit-box-shadow: 0px 0px 0.2px 0.2px rgba(0, 0, 0, 0.75);
      -moz-box-shadow: 0px 0px 0.2px 0.2px rgba(0, 0, 0, 0.75);
      box-shadow: 0px 0px 0.2px 0.2px rgba(0, 0, 0, 0.75);
      height: 20px;
    }
  }
  button {
    padding: 0px 30px;
    background-color: #04a399;
    border: none;
    color: white;
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