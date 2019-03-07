<template>
    <div v-if="pages > 1">
            <button class="btn" @click="goToInit()" v-if="showInit"> <i class="fa fa-fast-backward" aria-hidden="true"></i></button>
            <button class="btn" @click="goToPrev()" v-if="showPrev"> <i class="fa fa-step-backward" aria-hidden="true"></i></button>
            <button class="btn"> {{current + 1}} </button>
            <button class="btn" @click="goToNext()" v-if="showNext"> <i class="fa fa-step-forward" aria-hidden="true"></i></button>
            <button class="btn" @click="goToLast()" v-if="showLast"> <i class="fa fa-fast-forward" aria-hidden="true"></i></button>
        </div>
        <button v-else class="btn"> {{current + 1}} </button>
</template>
<script>
export default {
    props: [
        'pages', //Total number of pages,
        'current', // Current page viewing. Sync property
    ],

    data: function(){
        return {};
    },

    computed:{
        showInit: function () {
            if (this.current >= 2) {return true;}
            return false;
        },

        showPrev: function () {
            if (this.current >= 1) {return true;}
            return false;
        },

        showNext: function () {
            if ( this.current < (this.pages -1)) {return true;}
            return false;
        },

        showLast: function () {
            if ((this.pages-1) - this.current >= 2) {return true;}
            return false;
        }


    },

    methods: {
        goToInit: function () {
            this.$emit('update:current', 0); 
            this.$emit('change')
            
        },

        goToPrev: function () {
            this.$emit('update:current', this.current - 1); 
            this.$emit('change')
            
        },

        goToNext: function () {
            this.$emit('update:current', this.current + 1); 
            this.$emit('change')
            
        },

        goToLast: function () {
            this.$emit('update:current', this.pages - 1); 
            this.$emit('change')
            
        },
    }
}
</script>

