<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>
    import emit from '@/util/emitter.js'
    export default {
        name: "Form",
        props: {
            model: {
                type: Object,
                default: () => {
                    return {}
                }
            },
            rule: {
                type:Object,
                default: () => {
                    return {}
                }
            }
        },
        provide(){
          return{
              form:this
          }
        },
        data() {
            return {

            }
        },
    }
</script>

<style scoped>

</style>
