<template>
  <form  class="validate-form-container">
    <slot name="default"></slot>
    <div class="submit-area" @click.prevent="onSubmit">
      <slot name="submit">
        <button type="submit" class="btn btn-primary">提交</button>
      </slot>
    </div>
  </form>
</template>

<script lang="ts">
import { defineComponent, onUnmounted } from 'vue'
import mitt from 'mitt'
import { InputInstance } from './ValidateInput.vue'
export const mitter = mitt()
export interface FormInstance {
  onSubmit: () => void;
  resetForm: () => void;
}
type getInputInstance = () => InputInstance;
export default defineComponent({
  emits: ['form-submit'],
  setup (props, context) {
    let inputInstances: InputInstance[] = []
    const onSubmit = () => {
      const result = inputInstances.map(input => {
        input.validate()
      }).every(result => result)
      context.emit('form-submit', result)
    }
    const resetForm = () => {
      inputInstances.forEach(input => input.reset())
    }
    const callback = (inputInstance: InputInstance) => {
      inputInstances.push(inputInstance)   
    }
  
    mitter.on<any>('form-item-created', callback)
 
    onUnmounted(() => {
      mitter.off<any>('form-item-created', callback)
      inputInstances = []
    })
    return {
      onSubmit,
      resetForm
    }
  }
})
</script>

<style scoped>

</style>
