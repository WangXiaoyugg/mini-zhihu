<template>
  <div class="container">
    <global-header :user="currentUser"></global-header>
    <validate-form @form-submit="onFormSubmit" ref="formRef">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input 
          :rules="emailRules" 
          v-model="emailVal"
          placeholder="this is email"
          type='text'
        ></validate-input>
      </div>
      <div class="mb-3">
        <label class="form-label">密码</label>
        <validate-input 
          :rules="passwordRules" 
          v-model="passwordVal"
          placeholder="this is password"
          type='password'
        ></validate-input>
      </div>
      <template #submit>
        <button class="btn btn-danger">Submit</button>
      </template>
    </validate-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, Ref, ref } from 'vue'
import 'bootstrap/dist/css/bootstrap.min.css'
import GlobalHeader, { UserProps } from './components/GlobalHeader.vue'
import ValidateInput, { RulesProp } from './components/ValidateInput.vue'
import ValidateForm, { FormInstance } from './components/ValidateForm.vue'
const currentUser: UserProps = {
  isLogin: true,
  name: 'garen',
  id: 1
}
const emailRules: RulesProp = [
  { type: 'required', message: '电子邮箱地址不能为空' },
  { type: 'email', message: '请输入正确的电子邮箱' }
]
const passwordRules: RulesProp = [
  { type: 'required', message: '密码不能为空' }
]
export default defineComponent({
  name: 'App',
  components: {
    GlobalHeader,
    ValidateInput,
    ValidateForm
  },
  setup () {
    const emailVal = ref('garen')
    const passwordVal = ref('123')
    const formRef = ref<FormInstance| HTMLFormElement | null>(null)
    const onFormSubmit = (result: boolean) => {
      console.log('onFormSubmit', result)
      if (formRef.value) {
        formRef.value.resetForm()
      }
    }
    
    return {
      // list: testData,
      currentUser,
      emailVal,
      emailRules,
      passwordVal,
      passwordRules,
      onFormSubmit,
      formRef
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
