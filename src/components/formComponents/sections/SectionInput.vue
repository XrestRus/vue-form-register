<template>
    <label class="section"
           :title="title"
           :for="name"
    >
        <span class="title">{{ title }}</span>
        <input class="value"
               :type="type"
               :id="name"
               :name="name"
               :value="modelValue"
               @input="e => $emit('update:modelValue', e.target.value)"
        />
        <error-template :errors="errors" />
    </label>
</template>

<script>
    import ErrorTemplate from "./sectionComponents/ErrorTemplate";
    export default {
        name: "SectionInput",
        components: {ErrorTemplate},
        props: {
            title: {
                type: String,
                default: ""
            },
            name: {
                type: String,
                default: ""
            },
            type: {
                type: String,
                default: "text"
            },
            modelValue: {
                type: String,
                default: null
            },
            errors: {
                type: Array,
                default: null
            }
        },

        emits: [
            'update:modelValue'
        ],
    }
</script>

<style lang="sass" scoped>
    @import ./src/sass/_shared.sass

    .section
        display: flex
        flex-direction: column
        margin: 1rem 0
        @extend %template-action-effect

        .value,
        .title
            @extend %template-section-item

        .value
            border-top: 1px solid var(--color-line)
            border-bottom: 1px solid var(--color-line)

</style>