<template>
  <v-container>
    <v-row>
      <v-col cols="6">
        <add-question-with-options-form @question-added="addQuestion"></add-question-with-options-form>
      </v-col>
      <v-col cols="6">
        <PreviewComponent :questions="questions"
          @delete-option="deleteOptionFromCard"
          @delete-question="deleteQuestion"></PreviewComponent>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import AddQuestionWithOptionsForm from './AddQuestionWithOptionsForm.vue';
import PreviewComponent from './PreviewComponent.vue';

export default {
  components: {
    AddQuestionWithOptionsForm,
    PreviewComponent,
  },
  data() {
    return {
      questions: [],
    };
  },
  methods: {
    addQuestion(newQuestion) {
      this.questions.push(newQuestion);
    },
    deleteOptionFromCard(qIndex, oIndex) {
      this.questions[qIndex].options.splice(oIndex, 1);
    },
    deleteQuestion(index) {
      this.questions.splice(index, 1);
    },
  },
};
</script>
