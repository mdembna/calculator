<template>
  <div class="calculator">
    <mdb-card class="display">{{current || '0'}}</mdb-card>
    <div>
      <mdb-btn class="number" color="blue-grey" @click="clear">AC</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="blue-grey" @click="sign">+/-</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="blue-grey" @click="percent">%</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="default" @click="divide">/</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('7')">7</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('8')">8</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('9')">9</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="default" @click="multiply">x</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('4')" >4</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('5')">5</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('6')">6</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="default" @click="substract">-</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('3')">3</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('2')">2</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="append('1')">1</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="default" @click="add">+</mdb-btn>
    </div>
    <div class="zero">
      <mdb-btn class="number" outline="default" @click="appendZero" >0</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" outline="default" @click="dot">.</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" color="default" @click="equal">=</mdb-btn>
    </div>
  </div>
</template>

<script>
import { mdbBtn, mdbCard } from "mdbvue";

export default {
  name: "Calculator",
  components: {
    mdbBtn,
    mdbCard
  },
  data() {
    return {
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false,
    };
  },
  methods: {
    clear() {
      this.current = "";
    },
    sign() {
      if (this.current !== "") {
        this.current = `${-parseFloat(this.current)}`;
      }
    },
    percent() {
      if (this.current !== "") {
        this.current = `${parseFloat(this.current) / 100}`;
      }
    },
    append(number) {
      if(this.operatorClicked){
        this.current = "";
        this.operatorClicked = false;
      }

      this.current = `${this.current}${number}`;
    },
    appendZero() {
      if (this.current.length > 0){
      this.current = `${this.current}0`;
      }
    },
    dot() {
      if(this.current.indexOf(".") === -1){
        if(this.current === ""){
          this.current = '0'
        }
        this.current = `${this.current}.`;
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add(){
      this.operator = (a, b) => a + b
      this.setPrevious()
    },
    substract(){
      this.operator = (a, b) => a - b
      this.setPrevious()
    },
    multiply(){
      this.operator = (a, b) => a * b
      this.setPrevious()
    },
    divide(){
      this.operator = (a, b) => a / b
      this.setPrevious()
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`
    }
  }
};
</script>




<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}

.display {
  grid-column: 1 / 5;
  justify-content: end;
}

.number {
  border-radius: 17.1rem;
  width: 100%;
}

.zero {
  grid-column: 1 / 3;
}
</style>
