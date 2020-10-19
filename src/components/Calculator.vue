<template>
  <div class="calculator">
    <div class="display item">{{ current }}</div>
    <div @click="clear" class="item btn">C</div>
    <div @click="takeRoot" class="item btn">√</div>
    <div @click="append('%')" class="item btn">%</div>
    <div @click="append('/')" class="item btn operators">÷</div>
    <div @click="append('7')" class="item btn">7</div>
    <div @click="append('8')" class="item btn">8</div>
    <div @click="append('9')" class="item btn">9</div>
    <div @click="append('*')" class="item btn operators">x</div>
    <div @click="append('4')" class="item btn">4</div>
    <div @click="append('5')" class="item btn">5</div>
    <div @click="append('6')" class="item btn">6</div>
    <div @click="append('-')" class="item btn operators">-</div>
    <div @click="append('1')" class="item btn">1</div>
    <div @click="append('2')" class="item btn">2</div>
    <div @click="append('3')" class="item btn">3</div>
    <div @click="append('+')" class="item btn operators">+</div>
    <div @click="append('0')" class="zero btn item">0</div>
    <div @click="append('.')" class="item btn">.</div>
    <div @click="calculate()" class="item btn operators">=</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: "100",
      operator: null,
    };
  },
  methods: {
    clear() {
      this.current = "0";
    },
    takeRoot() {
      this.current = `${Math.sqrt(this.current)}`;
    },
    percent() {
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(num) {
      if (isNaN(this.current[this.current.length - 1]) && isNaN(num)) {
        return;
      }

      if (this.current != "0") {
        this.current = `${this.current}${num}`;
      } else {
        this.current = num;
      }
    },
    dot() {
      if (this.current.indexOf(".") === -1) {
        this.append(".");
      }
    },
    calculate() {
      this.current = eval(this.current);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.item {
  border: 1px solid black;
  border-radius: 4px;
}
.calculator {
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  text-align: center;
  grid-column: 1 / 5;
  background-color: gray;
}
.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #eee;
}
.operators {
  background-color: orange;
  color: white;
}
</style>