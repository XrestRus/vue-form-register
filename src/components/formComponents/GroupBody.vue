<template>
    <div class="group-body">
        <slot>

        </slot>
    </div>
</template>

<script>
    export default {
        name: "GroupBody",
        components: {
        }
    }
</script>

<style lang="sass" scoped>
    .group-body
        margin: 1rem
        display: flex
        flex-direction: column
        flex: 1
        padding: .5rem

</style>