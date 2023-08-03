<template>
  <div>
    <input type="number" v-model="numero1" @input="calcular">
    <input type="number" v-model="numero2" @input="calcular">

    <div>
      <button @click="calcularOperacao('+')">+</button>
      <button @click="calcularOperacao('-')">-</button>
      <button @click="calcularOperacao('*')">*</button>
      <button @click="calcularOperacao('/')">/</button>
    </div>

    <div v-if="resultado !== null || mensagemErro">
      <p v-if="mensagemErro">{{ mensagemErro }}</p>
      <p v-else>Resultado: {{ resultado }}</p>
    </div>
  </div>
</template>

<script>
export default {
    name: "CalculadoraComponent",
  data() {
    return {
      numero1: null,
      numero2: null,
      resultado: null,
      mensagemErro: "",
    };
  },
  methods: {
    calcular() {
      this.resultado = null;
      this.mensagemErro = "";
    },
    calcularOperacao(operacao) {
      const num1 = parseFloat(this.numero1);
      const num2 = parseFloat(this.numero2);
      this.mensagemErro = "";

      switch (operacao) {
        case "+":
          this.resultado = num1 + num2;
          break;
        case "-":
          this.resultado = num1 - num2;
          break;
        case "*":
          this.resultado = num1 * num2;
          break;
        case "/":
          if (num2 === 0) {
            this.mensagemErro = "Divisão por 0 não é possível!";
            this.resultado = null;
          } else {
            this.resultado = num1 / num2;
          }
          break;
        default:
          this.resultado = null;
          break;
      }
      if(isNaN(this.resultado)) {
        this.resultado = null;
      }
    },
  },
};
</script>
