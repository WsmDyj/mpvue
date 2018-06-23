<template>
    <div class="food" v-show="showFlag"></div>
</template>

<script>
export default {
    props: {
       food: {
            type: Object
        }
    }
}
</script>

<style lang="stylus" scoped>
    .food {
        position fixed
        left 0
        z-index 30
    }
</style>
