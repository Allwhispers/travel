<template>
    <input type="text" :value="currentValue" @input="handleInput" @blur="handleBlur">
</template>

<script>
    import emit from '@/util/emitter.js'
    export default {
        name: "FInput",
        data() {
            return {
                currentValue: "哈哈"
            }
        },
        mixins:[emit],
        props: ['value'],
        methods: {
            handleInput(ev) {
                const value = ev.target.value;
                this.currentValue = value;
                this.$emit('input',value);
                this.dispatch('FormItem','onInput',value)
            },
            handleBlur(){
                this.dispatch('FormItem','onBlur',this.currentValue);
            }
        },
    }
</script>

<style scoped>

</style>
