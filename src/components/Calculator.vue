<template>
  <div class="calculator">
    <div class="display"> {{ current || '0' }} </div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="negate">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div class="btn operator" @click="divide">/</div>
    <div class="btn" @click="append('7')">7</div>
    <div class="btn" @click="append('8')">8</div>
    <div class="btn" @click="append('9')">9</div>
    <div class="btn operator" @click="multiply">x</div>
    <div class="btn" @click="append('4')">4</div>
    <div class="btn" @click="append('5')">5</div>
    <div class="btn" @click="append('6')">6</div>
    <div class="btn operator" @click="substract">-</div>
    <div class="btn" @click="append('1')">1</div>
    <div class="btn" @click="append('2')">2</div>
    <div class="btn" @click="append('3')">3</div>
    <div class="btn operator" @click="add">+</div>
    <div class="btn zero" @click="append('0')">0</div>
    <div class="btn" @click="decimal">.</div>
    <div class="btn operator"  @click="equal">=</div>
    
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  props: {
  },
  data(){
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false
    }
  },
  methods: {
    clear() {
        this.current = '';
    },
    negate(){
        this.current = this.current.charAt(0) === '-' ?
         this.current.slice(1) : this.current.charAt(0) !== '0' &&  this.current.charAt(0) !== '' ? `-${this.current}` : this.current;
    },
    percent(){
      this.current = `${parseFloat(this.current) / 100}`;
    },
    append(num){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = this.current.charAt(0) !== '' && this.current.charAt(0) !== '0' ? 
        `${this.current}${num}` : this.current.charAt(1) !== '.' ? num : `${this.current}${num}`;
    },
    decimal(){
      if(this.current.indexOf('.') === -1){
        this.current = this.current === '' ? '0.' : this.current + '.';
      }
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    multiply(){
      this.operator = (a, b) => a * b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    substract(){
      this.operator = (a, b) => a - b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    add(){
      this.operator = (a, b) => a + b;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    equal(){
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.previous = null;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator {
  width: 400px;
  margin: 0 auto;
  font-size: 40px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background: lightblue;
  border:1px solid grey;
  color: white;
  text-align: right;
  padding-right: 10px;
}
.zero {
  grid-column: 1 / 3;
}
.btn{
  background: lightgrey;
  border:1px solid #999;
  color:black;
  cursor: pointer;
}
.btn:hover{
  background: blue;
}
.operator{
  background: orange;
  color:white;
}
</style>
