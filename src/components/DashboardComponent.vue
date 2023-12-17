<template>
  <div class="bg-grey-lighten-5" style="height:100vh">
      <div class="text-center py-10">
        <h1 class="text-blue">Hybrid Media</h1>
        <h1 class="text-green">Vue JS Assessment</h1>
      </div>

      <AddQuestions />
  </div>
</template>

<script>
import AddQuestions from './AddQuestionWithOptionsPage.vue';
export default {
  components: {
    AddQuestions,
  }
}
</script>

<style>

</style>