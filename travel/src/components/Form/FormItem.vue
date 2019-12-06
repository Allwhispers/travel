<template>
    <div>
        <label v-if="label">{{label}}</label>
        <slot></slot>
        <div v-if="validateState==='error'">{{validateMessage}}</div>
    </div>
</template>

<script>
    import emit from '@/util/emitter.js'
    import AsyncValidator from 'async-validator'

    export default {
        name: "FormItem",
        mixins:[emit],
        inject:['form'],
        props: {
            label: {
                type: String,
                default: ""
            },
            prop:{
                type:String,
                default: ""
            }
        },
        computed: {
            fieldValue() {
                console.log(this.form.model)
                return this.form.model[this.prop];
            }
        },
        methods: {
            getFilteRuleByTrigger(trigger) {
                return this.getRule().filter(item => {
                    return !item.trigger || item.trigger.includes(trigger)
                });
            },
            setRule(){
                this.$on('onBlur', this.onFieldBlur);
                this.$on('onInput', this.onFieldInput);
            },
            getRule(){
                console.log(this.form.rule[this.prop]);
                return this.form.rule[this.prop] ? [].concat(this.form.rule[this.prop]) : [];
            },
            validator(trigger,cb){
                let rules = this.getFilteRuleByTrigger(trigger);
                if(!rules || rules.length === 0){
                    return true
                }
                let desc = {};
                desc[this.prop] = rules;
                const validator = new AsyncValidator(desc);
                let model = {};
                model[this.prop] = this.form.model[this.prop];
                validator.validate(model,{ firstFields: true }, error=>{
                    this.validateState = !errors ? 'success' : 'error';
                    this.validateMessage = errors ? errors[0].message : '';
                    if(cb){
                        cb(this.validateMessage);
                    }

                })

            },
            onFieldBlur(){
                this.validator('blur')
            },
            onFieldInput(){
                this.validator('input')
            }
        },
        data() {
            return {
                validateState: "",
                validateMessage: ""
            }
        },
        mounted(){
            if(this.prop){
                this.dispatch('addForm','Form',this);
                this.setRule();
            }
        }
    }
</script>

<style scoped>

</style>
