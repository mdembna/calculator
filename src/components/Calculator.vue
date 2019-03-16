<template>
  <div class="calculator">
    <mdb-card class="display">
      <div class="output">{{current || '0'}}</div>
    </mdb-card>
    <div>
      <mdb-btn class="number operator" @click="clear">AC</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number operator" @click="sign">+/-</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number operator" @click="percent">%</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number operator" @click="divide">/</mdb-btn>
    </div>

    <div :key="number" v-for="number in numbers[0]">
      <mdb-btn class="number" @click="append(number)">{{number}}</mdb-btn>
    </div>
  
    <div>
      <mdb-btn class="number operator" @click="multiply">x</mdb-btn>
    </div>

    <div :key="number" v-for="number in numbers[1]">
      <mdb-btn class="number" @click="append(number)">{{number}}</mdb-btn>
    </div>

    <div>
      <mdb-btn class="number operator" @click="substract">-</mdb-btn>
    </div>
        <div :key="number" v-for="number in numbers[2]">
      <mdb-btn class="number" @click="append(number)">{{number}}</mdb-btn>
    </div>

    <div>
      <mdb-btn class="number operator" @click="add">+</mdb-btn>
    </div>
    <div class="zero">
      <mdb-btn class="number number__zero" @click="appendZero">0</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number" @click="dot">.</mdb-btn>
    </div>
    <div>
      <mdb-btn class="number operator" @click="equal">=</mdb-btn>
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
      numbers: [["7", "8", "9"], ["4", "5", "6"], ["3", "2", "1"]],
      current: "",
      previous: null,
      operator: null,
      operatorClicked: false
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
      if (this.operatorClicked) {
        this.current = "";
        this.operatorClicked = false;
      }

      this.current = `${this.current}${number}`;
    },
    appendZero() {
      if (this.current.length > 0) {
        this.current = `${this.current}0`;
      }
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        if (this.current === "") {
          this.current = "0";
        }
        this.current = `${this.current}.`;
      }
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    substract() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    multiply() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      
    }
  }
};
</script>




<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
  width: 300px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(80px, auto);
}

.display {
  overflow: scroll;
  height: 120px;
  border-radius: 60px;
  grid-column: 1 / 5;
  margin: 0px 10px 50px 10px;
  padding: 0 30px;
  display: flex;
  justify-content: center;
  align-items: flex-end;
  font-size: 32px;
  font-weight: 600;
  background-color: rgba(255, 255, 255, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.6);
}
.output {
  overflow: scroll;
  width: 100%;
  display: flex;
  flex-wrap: nowrap;
}

.number {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  padding: 0px;
  margin: 10px;
  font-size: 20px;
  background-color: rgba(0, 0, 0, 0.6);
  border: 1px solid rgba(0, 0, 0, 0.6);
}

.number:focus {
  background-color: rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(0, 0, 0, 0.1);
  color: rgba(0, 0, 0, 0.8);
}

.operator {
  background-color: rgba(255, 255, 255, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.6);
  color: rgba(0, 0, 0, 0.8);
}

.operator:focus {
  background-color: rgba(0, 0, 0, 0.2);
  border: 1px solid rgba(0, 0, 0, 0.2);
  color: white;
}

.zero {
  grid-column: 1 / 3;
}

.number__zero {
  width: 140px;
  border-radius: 30px;
}

@media screen and (min-width: 420px){
  .calculator {
    padding-top: 100px;
    width: 400px;
  }

  .number {
    width: 80px;
    height: 80px;
  }
  .number__zero {
  width: 180px;
  border-radius: 40px;
}
}
</style>
