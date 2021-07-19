<template>
    <div class="wrap-form">
        <div class="form">
            <group-view />
        </div>
    </div>
</template>

<script>
    import GroupView from "./formComponents/GroupView"

    export default {
        name: 'FormView',

        components: {
            GroupView
        },

    }
</script>

<style lang="sass" scoped>

    .wrap-form
        display: flex
        background: white
        flex-direction: column
        position: relative

        .form-title
            text-align: center
            flex: .1
            justify-content: center
            align-items: center
            display: flex

        .form
            flex: 1
            background: white
            display: flex
            align-items: center
            justify-content: center
            margin: auto
            z-index: 1

</style>
