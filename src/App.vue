<template>
  <div id="app">
    <div id="wrapContent">
      <b-button-group>
        <b-button @click="actionButton('(?<tujuan>\\d+)')">Tujuan</b-button>
        <b-button @click="actionButton('(?<serial_number>.+)')"
          >Nomor Seri</b-button
        >
        <b-button @click="actionButton('(?<harga>.+)')">Harga</b-button>
        <b-button @click="actionButton('(?<saldo>.+)')">Saldo</b-button>
        <b-button @click="actionButton('(?<lewati>.+)')">Lewati</b-button>
        <b-button @click="actionButton('(?<keterangan>.+)')"
          >Keterangan</b-button
        >
      </b-button-group>
      <b-form>
        <b-form-group id="input-group-1" label-for="input-1">
          <b-form-textarea
            ref="ta"
            id="textarea"
            v-model="text"
            placeholder="Enter something..."
            rows="3"
            max-rows="6"
            @select="selectionHandler"
          ></b-form-textarea>
        </b-form-group>
      </b-form>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      text: "YUSCOM: PLNV50.32163298188 sdh pernah jam 18.50, status Sukses. SN/Ref: 6610-4376-7466-6846-5970/SUMANTRI/R1/450/110.60KWH. Trx ke-2/hr: PLNV50.2.32163298188.pin. Saldo 115.833.390",
      selectionRange: [],
    };
  },
  methods: {
    actionButton(reg) {
      if (this.selectionRange.length > 0) {
        let part1 = this.text.substring(0, this.selectionRange[0]);
        let part2 = this.text.substring(
          this.selectionRange[1],
          this.text.length
        );
        this.text = part1 + reg + part2;
        this.selectionRange = [];
      }
    },
    // focusHandler() {
    //   if (this.selectionRange[1] !== 0) {
    //     this.select();
    //   }
    // },
    selectionHandler(e) {
      this.selectionRange = [
        e.currentTarget.selectionStart,
        e.currentTarget.selectionEnd,
      ];
    },
    // blurHandler() {
    //   this.selectionRange = [0, 0];
    // },
    select() {
      this.$refs["ta"].setSelectionRange(
        this.selectionRange[0],
        this.selectionRange[1]
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #e0e6e9;
  height: 100vh;
  padding-top: 50px;
}
#wrapContent {
  width: 700px;
  margin: 0 auto;
}
</style>
