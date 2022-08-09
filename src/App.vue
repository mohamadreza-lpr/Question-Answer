<template>
      <div>
            <Header :index="this.headerIndex" :correctAnswers="corectCount" />
            <b-row>
                  <b-col cols="6" offset="3">
                        <Content :QuestionList="this.questionList[this.index]" :next="next" :increment="increment" />
                  </b-col>
            </b-row>
      </div>
</template>

<script>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";
import axios from "axios";
export default {
      name: "App",
      components: {
            Header: Header,
            Content: Content,
      },
      data() {
            return {
                  questionList: undefined,
                  index: 0,
                  corectCount: 0,
                  totalCount: 0,
            };
      },
      mounted() {
            this.getQuestions();
      },
      computed: {
            headerIndex() {
                  let headerIndex = this.index + 1;
                  return headerIndex;
            },
      },
      methods: {
            next() {
                  if (this.index < 9) {
                        this.index++;
                  }
            },
            getQuestions() {
                  axios.get("https://opentdb.com/api.php?amount=10&category=21&type=multiple", {
                        headers: {
                              "Content-type": "application/json",
                        },
                  }).then((response) => {
                        this.questionList = response.data.results;
                        console.log(this.questionList[this.index]);
                  });
            },
            increment(is_correct) {
                  if (is_correct) {
                        this.corectCount++;
                  }
                  this.totalCount++;
            },
      },
};
</script>

<style></style>
