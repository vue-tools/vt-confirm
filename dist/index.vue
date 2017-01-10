<style src="./style.css"></style>
<template src="./template.html"></template>
<script>
    import Vue from 'vue'
    import plugin from './plugin'

    let Component = {
        props: {
            visible: {
                type: Boolean,
                required: true
            }
        },
        data() {
            return {
                cancelAccess: false,
                confirmAccess: false
            }
        },
        methods: {
            confirmHandle(time) {
                setTimeout(() => {
                    this.confirmAccess = !this.confirmAccess
                }, time)
            },
            cancelHandle(time) {
                setTimeout(() => {
                    this.cancelAccess = !this.cancelAccess
                }, time)
            }
        }
    }

    Vue.use(plugin(Component))
    
    export default Component
</script>