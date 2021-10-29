<template>
  <ul>
    <learning-resource
      v-for="resourse in resources"
      :key="resourse.id"
      :id="resources.id"
      :title="resourse.title"
      :description="resourse.description"
      :link="resourse.link"
    ></learning-resource>
  </ul>
</template>

<script>
import LearningResource from './LearningResource.vue';

export default {
  name: 'StoredResources',
  inject: ['resources'],
  components: {
    LearningResource
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
