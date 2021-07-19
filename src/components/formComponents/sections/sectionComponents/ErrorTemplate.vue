<template v-if="errors?.length > 0">
     <span class="error"
           v-for="e of errors"
           :key="e.$uid"
     >
        {{ e.$message }}
    </span>
</template>

<script>
    export default {
        name: "ErrorTemplate",

        props: {
            errors: {
                type: Array,
                default: null
            }
        }
    }
</script>

<style lang="sass" scoped>
    .error
        border-bottom: 1px solid var(--color-line-error)
        width: 100%
        color: red
        padding: 0.5rem
        height: 40px
        font-size: 14px
</style>