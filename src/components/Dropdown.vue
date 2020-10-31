<template>
  <div class="dropdown">
    <a class="btn btn-outline-light my-2 dropdown-toggle" href="#" @click.prevent="toggleOpen">
      {{title}}
    </a>
    <div class="dropdown-menu" :style="{display: 'block'}" v-if="isOpen">
      <li class="dropdown-item" href="#">
        <a href="#">新建文章</a>
      </li>
      <li class="dropdown-item" href="#">
        <a href="#">编辑资料</a>
      </li>
    </div>
</div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'Dropdown',
  props: {
    title: {
      type: String,
      required: true
    }
  },
  setup () {
    const isOpen = ref(false)
    const toggleOpen = () => {
      isOpen.value = !isOpen.value
    }
    return {
      isOpen,
      toggleOpen
    }
  }
})
</script>

<style scoped>

</style>
