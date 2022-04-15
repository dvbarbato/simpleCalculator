<template>
  <div class="calculadora">
    <div class="display" >{{ valorCorrente || '0' }}</div>
    <div @click="limpar" class="botao">C</div>
    <div @click="sinal" class="botao">+/-</div>
    <div @click="porcentagem" class="botao">%</div>
    <div @click="dividir" class="botao operadores">÷</div>
    <div @click="juntarNumeros('7')" class="botao">7</div>
    <div @click="juntarNumeros('8')" class="botao">8</div>
    <div @click="juntarNumeros('9')" class="botao">9</div>
    <div @click="multiplicar" class="botao operadores">x</div>
    <div @click="juntarNumeros('4')" class="botao">4</div>
    <div @click="juntarNumeros('5')" class="botao">5</div>
    <div @click="juntarNumeros('6')" class="botao">6</div>
    <div @click="subtrair" class="botao operadores">-</div>
    <div @click="juntarNumeros('1')" class="botao">1</div>
    <div @click="juntarNumeros('2')" class="botao">2</div>
    <div @click="juntarNumeros('3')" class="botao">3</div>
    <div @click="somar" class="botao operadores">+</div>
    <div @click="juntarNumeros('0')" class="botao zero">0</div>
    <div @click="ponto" class="botao">.</div>
    <div @click="resultado" class="botao operadores">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      valorCorrente: '',
      numeroAnterior: null,
      operador: null,
      numeroClicado: false,
    };
  },
  methods: {

    limpar() {
      this.valorCorrente = '';
    },

    sinal() {
      this.valorCorrente = this.valorCorrente.charAt(0) === '-'
        ? this.valorCorrente.slice(1)
        : `-${this.valorCorrente}`;
    },

    porcentagem() {
      this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
    },

    juntarNumeros(numero) {
      if (this.numeroClicado) {
        this.valorCorrente = '';
        this.numeroClicado = false;
      }
      this.valorCorrente = `${this.valorCorrente}${numero}`;
    },

    ponto() {
      if (this.valorCorrente.indexOf('.') === -1) {
        this.juntarNumeros('.');
      }
    },

    setarValor() {
      this.numeroAnterior = this.valorCorrente;
      this.numeroClicado = true;
    },

    dividir() {
      this.operador = (num1, num2) => num1 / num2;
      this.setarValor();
    },

    multiplicar() {
      this.operador = (num1, num2) => num1 * num2;
      this.setarValor();
    },

    subtrair() {
      this.operador = (num1, num2) => num1 - num2;
      this.setarValor();
    },

    somar() {
      this.operador = (num1, num2) => num1 + num2;
      this.setarValor();
    },

    resultado() {
      this.valorCorrente = `${this.operador(
        parseFloat(this.numeroAnterior),
        parseFloat(this.valorCorrente),
      )}`;
      this.numeroAnterior = null;
    },
  },

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculadora {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  margin: 0 auto;
  width: 350px;
  }

.display {
  grid-column: 1/5;
  background-color: black;
  color: white;
  }

.zero{
  grid-column: 1/3;
  }

.botao {
  background-color: #f2f2f2;
  border: 1px solid gray;
  }

.operadores {
  background-color: orange;
  color: white;
  }
</style>
