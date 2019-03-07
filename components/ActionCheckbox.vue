<template>
    <span class="pointer" v-if="value" aria-hidden="true" @click="click()">&#9745;</span>
    <span class="pointer" v-else aria-hidden="true" @click="click()">&#9746;</span>
</template>
<script>
// Requires fontawesome.com
export default {
    props: {
        value:{
            type: Boolean,
        }
    },

    model:{
        prop: 'value',
        event: 'click'
    },

    data: function () {
        return {};
    },


    computed: {
        
    },

    beforeMount: function () {},
    mounted: function () {},
    beforeDestroy: function () {},

    methods: {
        click: function () {
            this.$emit('click', !this.$props.value)
            // this.$emit('click');
        },
    }
}
</script>
<style>
.pointer{
    cursor: pointer;
}
</style>

