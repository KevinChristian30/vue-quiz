<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      ></div>
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group
      class="single-question"
      v-for="(question, index) in questions"
      :key="question.q"
      name="fade"
    >
      <template v-if="index === questionsAnswered">
        <div class="question">{{ question.q }}</div>
        <div
          class="answers"
          v-for="answer in question.answers"
          :key="answer.text"
        >
          <div class="answer" @click.prevent="selectAnswer(answer.is_correct)">
            {{ answer.text }}
          </div>
        </div>
      </template>
    </transition-group>
  </div>
</template>

<script>
export default {
  name: "Questions",
  props: {
    questions: Object,
    questionsAnswered: Number,
  },
  emits: ["question-answered"],
  methods: {
    selectAnswer(is_correct) {
      this.$emit("question-answered", is_correct);
    },
  },
};
</script>
