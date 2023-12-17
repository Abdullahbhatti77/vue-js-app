<template>
  <div>
    <v-card class="question-card" v-for="(question, qIndex) in questions" :key="qIndex" elevation="4">
      <v-card-title>
        <template v-if="!question.editMode">
          <span class="question-text">{{ question.text }}</span>
          <v-btn @click="toggleEditMode(qIndex)" icon variant="text" color="success">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
        </template>
        <template v-else>
          <v-text-field v-model="question.text" outlined></v-text-field>
          <v-btn @click="saveEditedQuestion(qIndex)" icon color="success" variant="text" class="mb-5">
            <v-icon>mdi-check</v-icon>
          </v-btn>
        </template>
      </v-card-title>

      <v-card-text v-if="!question.editMode">
        <v-row v-for="(option, oIndex) in question.options" :key="oIndex" class="option-row">
          <v-col cols="1">
            <span class="option-index">{{ String.fromCharCode(97 + oIndex).toLowerCase() }})</span>
          </v-col>
          <v-col cols="9">
            <span class="option-text">{{ option.text }}</span>
          </v-col>
          <v-col cols="2">
            <v-btn @click="deleteOption(qIndex, oIndex)" color="red" icon variant="tonal" class="ml-5">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-col>
        </v-row>
        <v-btn @click="deleteQuestion(qIndex)" color="red" class="mt-5">Delete Question</v-btn>
      </v-card-text>

    </v-card>
  </div>
</template>

<script>
export default {
  props: {
    questions: Array,
  },
  methods: {
    deleteOption(qIndex, oIndex) {
      this.$emit('delete-option', qIndex, oIndex);
    },
    deleteQuestion(index) {
      this.$emit('delete-question', index);
    },
    toggleEditMode(qIndex) {
      this.questions[qIndex].editMode = !this.questions[qIndex].editMode;
    },
    saveEditedQuestion(qIndex) {
      this.questions[qIndex].editMode = false;
    },
  },
};
</script>

<style scoped>
.question-card {
  margin-bottom: 20px;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
}

.question-card .v-card-title {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.question-card .question-text {
  font-weight: bold;
  font-size: 18px;
}

.option-row {
  align-items: center;
  border-top: 1px solid #e0e0e0;
  padding-top: 10px;
}

.option-text {
  font-size: 16px;
}
.option-index {
  font-weight: bold;
  font-size: 16px;
}

</style>
