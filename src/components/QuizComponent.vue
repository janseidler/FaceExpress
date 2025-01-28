<template>
  <div class="quiz-container">
    <h1>FaceExpress</h1>
    <img :src="currentImage" alt="Microexpression" class="microexpression-image" />
    <div class="options">
      <button v-for="option in options" :key="option" @click="checkAnswer(option)">
        {{ option }}
      </button>
    </div>
    <p v-if="feedback">{{ feedback }}</p>
    <button @click="nextQuestion" v-if="feedback">Next</button>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const emotions = ['Happiness', 'Anger', 'Sadness', 'Contempt', 'Disgust', 'Fear', 'Surprise'];
    const currentEmotion = ref('');
    const currentImage = ref('');
    const options = ref([]);
    const feedback = ref('');

    const loadQuestion = () => {
      const emotion = emotions[Math.floor(Math.random() * emotions.length)];
      const imageNumber = Math.floor(Math.random() * 50) + 1;
      currentEmotion.value = emotion;
      currentImage.value = `/Microexpressions/${emotion}/${emotion}-Microexpression-${String(imageNumber).padStart(3, '0')}.jpeg`;
      options.value = shuffle([emotion, ...emotions.filter(e => e !== emotion)]);
      feedback.value = '';
    };

    const shuffle = (array) => {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    };

    const checkAnswer = (selectedOption) => {
      if (selectedOption === currentEmotion.value) {
        feedback.value = '✔️  Correct!';
      } else {
        feedback.value = `❌ Incorrect. It was ${currentEmotion.value}.`;
      }
    };

    const nextQuestion = () => {
      loadQuestion();
    };

    onMounted(() => {
      loadQuestion();
    });

    return {
      currentImage,
      options,
      feedback,
      checkAnswer,
      nextQuestion,
    };
  },
};
</script>

<style scoped>
.quiz-container {
  text-align: center;
}
.microexpression-image {
  width: 300px;
  height: auto;
}
.options button {
  margin: 5px;
}
</style>

