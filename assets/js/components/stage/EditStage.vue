<template>
<div class="container">
    <stage-form :stage="stage" v-bind:httpFunction="put">
      <div slot="button">
        <save-button slot="button" v-bind:itemToEdit="stage" class="ml-2 mb-2 mr-2 btn-sm"></save-button>
        <slot name="cancel-button"></slot>
      </div>
    </stage-form>
</div>
</template>

<script>
import axios from 'axios';
import StageForm from './StageForm.vue';
import SaveButton from '../button/SaveButton.vue'

export default {
  components: {
    'stage-form': StageForm,
    'save-button': SaveButton,
  },
  props: {
    stage: {
      type: Object,
      required: true
    },
    isEditing: {
      type: Boolean,
      required: true
    },
    goalId: {
      type: Number,
      required: true
    }
  },
  methods: {
    put() {
      this.stage.goalId = this.goalId
      this.$store.dispatch('editStage', this.stage)
        .then(() => {
          if(!this.hasErrors) {
            this.$emit('update:isEditing', false)
          }
        })
    },
  },
  computed: {
    hasErrors () {
      return this.$store.getters.hasErrors
    },
  }
}
</script>

<style scoped>

</style>
