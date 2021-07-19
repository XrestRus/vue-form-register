<template>
    <form-view />
</template>

<script>
    import FormView from './components/FormView'

    export default {
        name: 'App',
        components: {
            FormView
        }
    }
</script>

<style lang="sass">
    @import ./src/sass/_shared.sass

    #app
        overflow: hidden
        justify-content: center
        display: flex
        min-height: 100vh
</style>
