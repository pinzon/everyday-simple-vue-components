<template>
    <i v-if="value" class="fa fa-check-square-o" aria-hidden="true" @click="click()"></i>
    <i v-else class="fa fa-square-o" aria-hidden="true" @click="click()"></i>
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
