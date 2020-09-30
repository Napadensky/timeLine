<template>
  <div class="container">
    <h3>Agenda de reservas</h3>
    <div class="grid">
      <div class="left">
        <!-- <i class="material-icons dp48 buttons-menu" id="moveLeft">arrow_back</i> -->
        <i class="material-icons dp48" id="moveLeft"> chevron_left </i>
      </div>
      <div id="visualization">
        <div class="menu">
          <input
            style="display: none"
            id="sliderZoom"
            type="range"
            class="range"
            name="a"
            min="-1"
            max="1"
            step="0.1"
            value="0"
          />

          <i
            class="material-icons dp48 buttons-menu"
            id="fit"
            style="display: none"
            >home</i
          >
        </div>
      </div>
      <div class="right">
        <i class="material-icons dp48" id="moveRight">chevron_right</i>
      </div>
    </div>
  </div>
</template>

<script>
import vis from "vis";
import moment from "moment";

export default {
  props: ["reservas"],

  methods: {
    scriptTimeLine() {
      // create a timeline with some data
      let container = document.getElementById("visualization");
      let items = new vis.DataSet(this.reservas);
      let options = {
        //stack: false,
        orientation: {
          axis: "top",
          item: "top",
        },
        //zoomMax: 31536000000, // just one year
        zoomMax: 87600900, // 10,000 years is maximum possible
        zoomMin: 10000000, // 10ms
      };
      let timeline = new vis.Timeline(container, items, options);

      /**
       * Move the timeline a given percentage to left or right
       * @param {Number} percentage   For example 0.1 (left) or -0.1 (right)
       */
      function move(percentage) {
        let range = timeline.getWindow();
        let interval = range.end - range.start;
        timeline.setWindow({
          start: range.start.valueOf() - interval * percentage,
          end: range.end.valueOf() - interval * percentage,
        });
      }

      // attach events to the navigation buttons
      document.getElementById("moveLeft").onclick = function () {
        move(0.2);
      };
      document.getElementById("moveRight").onclick = function () {
        move(-0.2);
      };

      // Using slider to zoomIn or zoomOut
      document
        .getElementById("sliderZoom")
        .addEventListener("input", function (e) {
          var value = this.value;
          if (value < 0) {
            var start = moment().year(moment().year() - 100000), // to adjust with options
              end = moment().year(moment().year() + 1);
            timeline.zoomOut(-value);
            if (value === "-1") timeline.setWindow(start, end);
          } else if (value > 0) {
            var start = moment(),
              end = moment(moment().utc() + 10);
            timeline.zoomIn(value);
            if (value === "1") timeline.setWindow(start, end);
          } else {
            timeline.fit(items.getIds());
            this.value = 0;
          }
        });

      // To reset zoom initial state
      document.getElementById("fit").onclick = function () {
        //$('.range').next().text('0'); // set default if to use output with input range
        document.getElementById("sliderZoom").value = 0;
        timeline.fit(items.getIds());
      };
    },
  },

  computed: {
    reservaComputed() {
      console.log(this.reservas);
      return this.reservas;
    },
  },
  watch: {
    reservas: function (value) {
      // Eliminar elemento duplicado
      let oldcomp = document.getElementById("visualization").childNodes;
      oldcomp.length > 1 && oldcomp[1].remove();
      // console.log(oldcomp.length);
      this.scriptTimeLine();
    },
  },

  mounted() {
    this.scriptTimeLine();
  },
};
</script>

<style lang="scss" scoped>
.container {
  width: 85.6%;
  margin: auto;
  text-align: left;
  padding-top: 20px;
  padding-bottom: 20px;
  .grid {
    display: grid;
    grid-template-columns: 2.5% 95% 2.5%;
  }
  .left,
  .right {
    display: flex;
    align-items: center;
    justify-content: center;
    -webkit-box-shadow: 0px 0px 1px 0.5px rgba(0, 0, 0, 0.75);
    -moz-box-shadow: 0px 0px 1px 0.5px rgba(0, 0, 0, 0.75);
    box-shadow: 0px 0px 1px 0.5px rgba(0, 0, 0, 0.75);
  }
}
</style>