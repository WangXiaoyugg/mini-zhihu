<template>
  <li class="dropdown-option" :class="{'is-disabled': disabled}">
    <slot></slot>
  </li>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'DropdownItem',
  props: {
    disabled: {
      type: Boolean,
      default: false
    }
  },
  setup () {
    return {}
  }
})
</script>

<style>
.dropdown-option.is-disabled *{
  color: #6c757d;
  background: transparent;
  pointer-events: none;
}
</style>
