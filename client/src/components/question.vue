<template>
  <div class="question">
    <div class="head">
      <h1 style="text-align:left" v-text="this.$store.state.detailQuestion.title"></h1>
    </div>
    <div class="body">
      <div class="vote">
        <i
          class="fas fa-caret-down fa-2x"
          style="transform : rotate(180deg)"
          @click="questionUpvote()"
        ></i>
        <h3>{{this.$store.state.detailQuestion.upvote.length - this.$store.state.detailQuestion.downvote.length }}</h3>
        <i class="fas fa-caret-down fa-2x" @click="questionDownvote()"></i>
      </div>
      <div class="description">
        <p style="text-align:left" v-html="this.$store.state.detailQuestion.description"></p>
      </div>
    </div>
    <div class="head">
      <div class="answer">
        <h4 style="text-align:left">({{this.$store.state.detailQuestion.answer.length}}) Answer</h4>
      </div>
    </div>
    <div
      class="body body-answer"
      v-for="(answ, index) in this.$store.state.detailQuestion.answer"
      :key="index"
    >
      <div class="vote">
        <i
          class="fas fa-caret-down fa-2x"
          style="transform : rotate(180deg)"
          @click="answerUpvote(answ._id)"
        ></i>
        <h3>{{answ.upvote.length - answ.downvote.length}}</h3>
        <i class="fas fa-caret-down fa-2x" @click="answerDownvote(answ._id)"></i>
      </div>
      <div class="description">
        <p style="text-align:left">{{answ.description}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  created() {
    this.$store.dispatch("getAllQuestion");
  },
  methods: {
    questionUpvote() {
      let id = this.$store.state.detailQuestion._id;
      this.$store.dispatch("questionUpvote", id);
    },
    questionDownvote() {
      let id = this.$store.state.detailQuestion._id;
      this.$store.dispatch("questionDownvote", id);
    },
    answerUpvote(id) {
      this.$store.dispatch("answerUpvote", id);
    },
    answerDownvote(id) {
      this.$store.dispatch("answerDownvote", id);
    }
  }
};
</script>

<style scoped>
.question {
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  width: 80vw;
}

.answer {
  width: 100%;
}

.body-answer {
  border-bottom: 1px solid #aaa;
  margin-bottom: 20px;
}

.head {
  margin: 20px;
  width: 100%;
  border-bottom: 1px solid #000;
}

.body {
  width: 100%;
  display: flex;
}

.vote {
  width: 100px;
}
</style>