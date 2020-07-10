<template>
  <div class="conversor">
    <img alt="Vue logo" class="text-center" src="./../assets/money.png" />
    <h2 v-if="convert">{{ moedaA }} {{ to }} {{ moedaB }}</h2>
    <h2 v-if="!convert">Carregando...</h2>
    <input type="number" v-model="moedaA_value" v-bind:placeholder="moedaA" />
    <input type="button" value="Converter" v-on:click="converter" />
    <h2>{{ moedaB_value }}</h2>
  </div>
</template>

<script>
export default {
  name: "conversor",
  props: ["moedaA", "moedaB"],

  data() {
    return {
      to: "Para",
      moedaA_value: 1,
      moedaB_value: 0,
      convert: true
    };
  },
  mounted: function() {
    this.$nextTick(function() {
      this.converter();
    });
  },
  methods: {
    converter() {
      if (this.moedaA_value == "") {
        alert("Digite um valor");
      } else {
        let apiKey = "96fd3e366a24ab0de23a";
        let from_to = `${this.moedaA}_${this.moedaB}`;
        let url = `https://free.currconv.com/api/v7/convert?q=${from_to}&compact=ultra&apiKey=${apiKey}`;

        this.convert = false;

        fetch(url)
          .then(res => {
            return res.json();
          })
          .then(json => {
            let value = json[from_to];

            switch (this.moedaA) {
              case "USD":
                this.moedaB_value =
                  "R$ " + (value * parseFloat(this.moedaA_value)).toFixed(2);
                break;

              case "CAD":
                this.moedaB_value =
                  "R$ " + (value * parseFloat(this.moedaA_value)).toFixed(2);
                break;

              case "EUR":
                this.moedaB_value =
                  "R$ " + (value * parseFloat(this.moedaA_value)).toFixed(2);
                break;
            }

            switch (this.moedaB) {
              case "USD":
                this.moedaB_value =
                  "$ " + (value * parseFloat(this.moedaA_value)).toFixed(2);
                break;

              case "CAD":
                this.moedaB_value =
                  "C$ " + (value * parseFloat(this.moedaA_value)).toFixed(2);
                break;

              case "EUR":
                this.moedaB_value =
                  "€ " + (value * parseFloat(this.moedaA_value)).toFixed(2);
                break;
            }

            this.convert = true;
            this.moedaA_value = "";
          });
      }
    }
  }
};
</script>

<style scoped>
.conversor {
  padding: 20px;
  margin: 20px;
  max-width: 300px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  border-radius: 7px;
  background: #fff;
}

.conversor h2 {
  padding: 5px;
}

.conversor img {
  max-width: 40px;
  padding: 10px;
}
</style>
