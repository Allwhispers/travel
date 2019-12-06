<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <w-form v-model="formData" :rule="ruleValidate">
      <w-formItem label="姓名" prop="name">
        <w-input v-model="formData.name"></w-input>
      </w-formItem>
      <w-formItem label="密码" prop="pwd">
        <w-input v-model="formData.pwd"></w-input>
      </w-formItem>
    </w-form>

    <button @click="handle">测试</button>
  </div>
</template>

<script>
// @ is an alias to /src

import HelloWorld from '@/components/HelloWorld.vue'
import WForm from '@/components/Form/Form.vue'
import WFormItem from '@/components/Form/FormItem.vue'
import WInput from '@/components/Form/FInput'
export default {
    name: 'home',
    data(){
        return{
            formData:{
                name: 'wangli',
                pwd:'123'
            },
            ruleValidate: {
                name: [
                    { required: true, message: '用户名不能为空', trigger: 'blur' }
                ],
                pwd: [
                    { required: true, message: '邮箱不能为空', trigger: 'blur' },
                    { type: 'email', message: '邮箱格式不正确', trigger: 'blur' }
                ],
            }
        }
    },
    methods:{
        handle(){
            console.log(this.formData)
        }
    },
    created(){
        console.log('homeCreated')
    },
    mounted(){
        console.log('homemounted')
    },
    components: {
        HelloWorld,
        WForm,
        WFormItem,
        WInput
    },
}
</script>
