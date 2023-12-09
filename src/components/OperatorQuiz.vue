<template>
  <div>
    <div v-if="isQuizStart" class="mb-3">
      <h3 class="text-dark">
        {{ operandLeft }} {{ operator }} {{ operandRight }}
      </h3>
    </div>
    <div class="col-12 d-flex justify-content-evenly align-items-center">
      <button
        @click="selectAnswer(answer)"
        :style="{ width: '100px' }"

        :class="{ 'green': selectedAnswer && answer === correctAnswer, 'yellow': !success && answer !== correctAnswer, 'blue':  selectedAnswer == null, }"
        class="btn  btn-lg text-white  "
        v-for="(answer, index) of answers"
        :key="index"
      >
        {{ answer }}
      </button>
    </div>
    <div v-if="!isQuizStart" class="col-12 d-flex justify-content-evenly align-items-center mb-5">
      <button
        class="btn btn-lg" 
        v-for="(chooseAnswer, index) of chooseAnswers"
        :key="index"
        :class="{ 'green': chooseAnswer== 'true', 'red': chooseAnswer == 'false', }"
      >
        {{index+1}}
      </button>
    </div>
    <div class="col-12 d-flex justify-content-center align-items-center mt-3">
      <button
        v-if="!isQuizStart && chooseAnswers.length < 4"
        @click="stratQuiz"
        class="btn btn-success btn-lg"
      >
        Start
      </button>
      <button
        :style="{ marginLeft: '40px' }"
        @click="$emit('onBack')"
        class="btn btn-warning btn-lg"
      >
        Back
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "OperatorQuiz",
  props: ["operator"],
  data() {
    return {
      isQuizStart: false,
      operandLeft: null,
      operandRight: null,
      answers: [],
      correctAnswer: null,
      selectionCounter: 0,
      info:true,
      success:false,
      selectedAnswer: null,
      chooseAnswers:[],
    
    };
  },
  methods: {
    selectAnswer(selectedAnswer) {
      this.selectionCounter++;
      this.selectedAnswer = selectedAnswer;
      if(selectedAnswer !=this.correctAnswer)
      {
        this.chooseAnswers.push('false')
      }else{
        this.chooseAnswers.push('true')
      }
      console.log(this.chooseAnswer);
      setTimeout(()=>{
        this.selectedAnswer=null;
        if (this.selectionCounter >= 5) {
        this.isQuizStart = false;
       
        this.answers = [];
        this.selectionCounter = 0;
      } else if (selectedAnswer !== this.correctAnswer) {
        console.log("IncorrectAnswer");
        this.stratQuiz();
      } else {
        console.log("correctAnswer");
        this.stratQuiz();
      }
      },500)
      

      
    },
    stratQuiz() {
      this.isQuizStart = true;
      this.operandLeft = parseInt(Math.random() * 13);
      this.operandRight = parseInt(Math.random() * 13);
      let correctAnswer;
      switch (this.operator) {
        case "+":
          correctAnswer = this.operandLeft + this.operandRight;
          break;
        case "-":
          correctAnswer = this.operandLeft - this.operandRight;
          break;
        case "*":
          correctAnswer = this.operandLeft * this.operandRight;
          break;
        case "/":
          correctAnswer = this.operandLeft / this.operandRight;
          break;
      }

      if (this.operator === "/") {
        correctAnswer = Number(correctAnswer.toFixed(2));
      }
      this.answers = [];
      this.answers.push(correctAnswer);
      this.correctAnswer = Math.floor(correctAnswer);
      for (let i = 0; i < 4; i++) {
        let sign = Math.random() < 0.5 ? -1 : 1;
        let offset = Math.floor(Math.random() * 3) * sign;
        let incorrectAnswer = Number((correctAnswer + offset).toFixed(2));
        while (
          incorrectAnswer === correctAnswer ||
          this.answers.includes(incorrectAnswer)
        ) {
          sign = Math.random() < 0.5 ? -1 : 1;
          offset = Math.floor(Math.random() * 3) * sign;
          incorrectAnswer =Number((correctAnswer + offset).toFixed(2)) ;
        }

        this.answers.push(incorrectAnswer);
      }
      this.answers = this.shuffleArray(this.answers);
    },

    shuffleArray(array) {
      console.log(array);
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    },
  },
};
</script>

<style scoped>

.green {
  background-color: #14A44D; 
}
.yellow {
  background-color: #E4A11B; 
}
.blue {
  background-color: #3B71CA;
}
.borderblue{
  border: 2px solid darkblue;
}
.red{
  background-color: red;
}
</style>
