<template>
  <div class="conversor">
    <img alt="Vue logo" class="text-center" src="./../assets/money.png" />
    <h2>{{ moedaA }} {{ to }} {{ moedaB }}</h2>
    <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaAvalue" />
    <input type="button" value="Converter" v-on:click="converter" />
    <h2>{{moedaB_value}}</h2>
  </div>
</template>

<script>
export default {
  name: "conversor",
  props: ["moedaA", "moedaB"],

  data() {
    return {
      to: "Para",
      moedaAvalue: this.moedaA,
      moedaA_value: "",
      moedaB_value: 0
    };
  },

  methods: {
    async converter() {
      if (this.moedaA_value == "") {
        alert("Digite um valor");
      } else {
        let from_to = `${this.moedaA}_${this.moedaB}`;
        let url = `https://free.currconv.com/api/v7/convert?q=${from_to}&compact=ultra&apiKey=3a1b8c53c13a6a68c088`;

        let cloneMoedaA = this.moedaA;
        let cloneMoedaB = this.moedaB;

        this.to = "Carregando ...";
        this.moedaA = "";
        this.moedaB = "";

        await fetch(url)
          .then(res => {
            return res.json();
          })
          .then(json => {
            let value = json[from_to];

            switch (cloneMoedaA) {
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

            switch (cloneMoedaB) {
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

            this.moedaA = cloneMoedaA;
            this.moedaB = cloneMoedaB;
            this.to = "Para";
            this.value_validation = "";
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