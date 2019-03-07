<template>
    <i v-if="state" class="fa fa-check-square-o" aria-hidden="true" @click="click()"></i>
    <i v-else class="fa fa-square-o" aria-hidden="true" @click="click()"></i>
</template>
<script>
// Requires fontawesome.com
export default {
    props: [
        'state', //bool
    ],

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
            this.$emit('click');
        },
    }
}
</script>
