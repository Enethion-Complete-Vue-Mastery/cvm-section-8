<template>
  <div class="ctr">
    <transition name="fade">
      <Questions
        v-if="questionsAnswered < questions.length"
        :questionsAnswered="questionsAnswered"
        :questions="questions"
        @answer-question="onAnswer"
      />
      <Result v-else :result="result" />
    </transition>
    <button type="button" class="reset-btn" @click="reset">Reset</button>
  </div>
</template>

<script>
import Result from './components/Result.vue'
import Questions from './components/Questions.vue'
export default {
  name: 'App',
  components: {
    Result,
    Questions
  },
  data () {
    return {
      questionsAnswered: 0,
      score: 0,
      questions: [
        {
          q: 'What is 2 + 2?',
          answers: [
            {
              text: '4',
              is_correct: true
            },
            {
              text: '3',
              is_correct: false
            },
            {
              text: 'Fish',
              is_correct: false
            },
            {
              text: '5',
              is_correct: false
            }
          ]
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: '5',
              is_correct: false
            },
            {
              text: '7',
              is_correct: false
            },
            {
              text: '6',
              is_correct: true
            },
            {
              text: '12',
              is_correct: false
            }
          ]
        },
        {
          q: 'Find the missing letter: C_ke',
          answers: [
            {
              text: 'e',
              is_correct: false
            },
            {
              text: 'a',
              is_correct: true
            },
            {
              text: 'i',
              is_correct: false
            }
          ]
        }
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: 'Try again!',
          desc: 'Do a little more studying and you may succeed!'
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: 'Studying has definitely paid off for you!'
        }
      ]
    }
  },
  methods: {
    onAnswer (isCorrect) {
      ++this.questionsAnswered
      this.score += isCorrect
    },
    reset () {
      this.questionsAnswered = 0
      this.score = 0
    }
  },
  computed: {
    result () {
      return this.results.find((r) => {
        return r.min <= this.score && r.max >= this.score
      })
    }
  }
}
</script>
