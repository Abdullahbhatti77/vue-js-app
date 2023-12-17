<template>
  <v-card elevation="4">
    <v-card-title>Add Question with Options</v-card-title>
    <v-card-text>
      <v-text-field v-model="newQuestion" label="Enter Question" outlined></v-text-field>
      <v-divider class="my-4"></v-divider>
      <v-row v-for="(option, index) in options" :key="index" class="mb-4">
        <v-col cols="1" class="mt-4">
          <span class="option-index">{{ String.fromCharCode(97 + index).toUpperCase() }})</span>
        </v-col>
        <v-col cols="6">
          <v-text-field v-model="option.text" label="Enter Option" outlined></v-text-field>
        </v-col>
        <v-col cols="3">
          <v-checkbox v-model="option.isCorrect" label="Correct" color="green"></v-checkbox>
        </v-col>
        <v-col cols="2" class="mt-1">
          <v-btn @click="deleteOption(index)" color="red" icon variant="text">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-col>
      </v-row>
      <v-btn @click="addOption" color="blue" class="mr-4">Add Option</v-btn>
      <v-btn @click="addQuestion" :disabled="!isCorrectOptionSelected" color="green">Add Question</v-btn>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      newQuestion: '',
      options: [],
    };
  },
  computed: {
    isCorrectOptionSelected() {
      return this.options.some(option => option.isCorrect);
    },
  },
  methods: {
    addOption() {
      this.options.push({ text: '', isCorrect: false });
    },
    deleteOption(index) {
      this.options.splice(index, 1);
    },
    addQuestion() {
      if (this.newQuestion.trim() !== '' && this.isCorrectOptionSelected && this.options.length > 0) {
        const newQuestion = {
          text: this.newQuestion.trim(),
          options: JSON.parse(JSON.stringify(this.options)),
        };
        this.$emit('question-added', newQuestion);
        this.newQuestion = '';
        this.options = [];
      }
    },
  },
};
</script>

<style scoped>
.v-card-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 12px;
}
.mb-4 {
  margin-bottom: 16px;
}
.option-index {
  font-weight: bold;
  font-size: 16px;
}
</style>
