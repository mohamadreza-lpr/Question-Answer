<template class="bg-secondary">
      <div>
            <b-jumbotron class="m-2 bg-dark">
                  <template #header><h2 class="text-warning">Questions</h2></template>

                  <template #lead>
                        <p class="text-white">
                              {{ QuestionList.question }}
                        </p>
                  </template>

                  <hr class="my-4" />
                  <b-list-group>
                        <b-list-group-item
                              v-for="(answer, index) in answers"
                              :key="answer.index"
                              @click="answerIndex(index)"
                              :class="[
                                    currentListIndex == index && !answered ? 'selectedList' : 'notSelectedList',
                                    answered && index == correctAnswer ? 'correctAnswer' : '',
                                    answered && index !== correctAnswer ? 'incorrectAnswer' : '',
                              ]"
                        >
                              <h6>{{ answer }}</h6>
                        </b-list-group-item>
                  </b-list-group>
                  <b-button href="#" @click="SubmitAnswer" :disabled="currentListIndex == null">Submit</b-button>
                  <b-button href="#" @click="nextQuestion">NEXT</b-button>
            </b-jumbotron>
      </div>
</template>

<script>
import _ from "lodash";
export default {
      props: {
            QuestionList: Object,
            next: Function,
            increment: Function,
      },
      data() {
            return {
                  currentListIndex: null,
                  answered: false,
            };
      },
      watch: {
            QuestionList: {
                  immediate: true,
                  handler() {
                        this.answered = false;
                        this.currentListIndex = null;
                  },
            },
      },
      methods: {
            //change the index of the answer on every click
            answerIndex(index) {
                  this.currentListIndex = index;
            },
            SubmitAnswer() {
                  let is_correct = false;
                  let correctAnswerIndex = this.answers.indexOf(this.QuestionList.correct_answer);
                  if (correctAnswerIndex == this.currentListIndex) {
                        is_correct = true;
                  }
                  this.increment(is_correct);
                  this.answered = true;
            },
            nextQuestion() {
                  this.next();
            },
      },
      computed: {
            correctAnswer() {
                  let cAnswer = this.answers.indexOf(this.QuestionList.correct_answer);
                  return cAnswer;
            },
            answers() {
                  let Answers = [...this.QuestionList.incorrect_answers];
                  Answers.push(this.QuestionList.correct_answer);
                  return _.shuffle(Answers);
            },
      },
};
</script>

<style>
.btn {
      margin: 10px 2px;
      color: rgb(255, 217, 205);
}
.notSelectedList {
      font-weight: 500;
      color: rgb(61, 61, 61);
      transition: background-color 0.5s ease;
}
.notSelectedList:hover {
      background-color: rgb(255, 217, 0);
      color: rgb(0, 0, 0);
      font-weight: bolder;
}
.selectedList h6 {
      color: rgb(129, 131, 0);
      text-shadow: rgb(184, 11, 11);
      font-weight: 900;
      font-size: 20px;
      padding: 5px;
      text-align: center;
      transition: 0.5s ease-out;
}
.correctAnswer h6 {
      color: rgb(0, 220, 0);
      font-size: 20px;
      font-weight: 900;
      text-align: center;
}
.incorrectAnswer {
      color: rgb(220, 0, 0);
}
</style>
