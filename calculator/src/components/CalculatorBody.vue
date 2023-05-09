<template>
  <!-- Happy Coding -->
  <div class="calculator">
    
    <!-- Calculator Result -->
    <div class="result">
      {{ calculatorValue || 0 }}
    </div>

    <!-- Calculator buttons -->
    <div class="buttons">
      <div class="button" v-for="n in calculatorElements" :key="n"
        :class="{'operator': ['C','*','/','-','+','%','='].includes(n)}"
        @click="action(n)"
      >
        {{n}}
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'CalculatorBody',
  props: {
    msg: String
  },

  data() {
    return {
      calculatorValue: '',
      calculatorElements: ['C','*','/','-','+','%',7,8,9,4,5,6,1,2,3,0,'.','='],
      operator: null,
      previousCalculatorValue: '',
    }
  },

  methods: {
    action(n){

      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }

      if(n === 'C'){
        this.calculatorValue = '';
      }

      if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }

      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = '';
      }

      if(n === '='){
        if(this.calculatorValue !== null){
          this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        console.log(this.calculatorValue);
        
        this.previousCalculatorValue = '';
        this.operator = null;
        }else{
          console.log(this.calculatorValue);
        }
      }
    }
  }
}
</script>


<style lang="scss" scoped>

  //colors and hovers
  $background : #234;
  $resultColor : black;
  $resultBackground : whitesmoke;
  $buttonText : #fff;
  $buttonBackground : #31475e;
  $buttonHover : #4e647d;
  $operatorBackground : rgb(255, 132, 0);
  $operatorHover : rgb(255, 85, 0);

  //dimensions 

  .calculator {
  max-width: 400px;
  margin: 50px auto;
  background: $background;
  padding: 3rem;
  border-radius: 20px;

  .result {
    width: 90%;
    padding: 1rem;
    text-align: right;
    font-size: 2rem;
    font-weight: bold;
    color: $resultColor;
    background: $resultBackground;
    border-radius: 0.25rem;
    margin-bottom: 1rem;
  }

  .buttons {
    display: flex;
    flex-wrap: wrap;

    .button {
      flex: 1 1 25%;
      margin: 0.25rem;
      font-size: 1.5rem;
      font-weight: bold;
      color: $buttonText;
      background: $buttonBackground;
      border-radius: 0.25rem;
      display: flex;
      justify-content: center;
      align-items: center;
      cursor: pointer;
      transition: background-color 0.2s ease-in-out;

      &:hover {
        background-color: $buttonHover;
      }

      &.operator {
        background-color: $operatorBackground;

        &:hover {
          background-color: $operatorHover;
        }
      }
    }
  }
}
</style>
