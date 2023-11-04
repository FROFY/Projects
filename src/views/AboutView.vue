<template>
  <div>
    <h1>This is an about page11</h1>
    <project-page
      :showModal="showModal"
      @close="showModal = false"
    />
    <button @click="showModal = true">Show Dialog</button>
  </div>
</template>

<script>
import ProjectDialog from '@/components/ProjectDialog.vue';
export default {
  components: {
    'project-page': ProjectDialog
  },
  data() {
    return {
      showModal: true,
    }
  },
}
</script>