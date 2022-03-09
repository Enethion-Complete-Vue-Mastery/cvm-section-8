<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
      />
      <div class="status">
        {{ questionsAnswered }} out of {{ questions.length }} questions answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, qi) in questions"
        :key="qi"
        v-show="qi === questionsAnswered"
      >
        <div class="question" v-text="question.q" />
        <div class="answers">
          <div
            class="answer"
            v-for="answer in question.answers"
            :key="answer.text"
            v-text="answer.text"
            @click.prevent="$emit('answer-question', answer.is_correct)"
          />
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  props: ['questions', 'questionsAnswered'],
  emits: ['answer-question']
}
</script>
