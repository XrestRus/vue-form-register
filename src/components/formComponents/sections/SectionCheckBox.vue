<template>
    <label class="section--check"
           :title="title"
           :for="name"
    >
        <input class="value"
               type="checkbox"
               :name="name"
               :id="name"
               :checked="modelValue"
               @click="e => $emit('update:modelValue', !modelValue)"
        />
        <span class="title">{{ title }}</span>
    </label>
</template>

<script>
    export default {
        name: "SectionCheckBox",

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
                type: Boolean,
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

    .section--check,
    .section--check .title
        @extend %template-section-item

    .section--check
        @extend %template-action-effect

        border-bottom: 1px solid var(--color-line)
        font-size: 14px
        margin: 1rem 0

        .title
            padding-left: 0.5rem
</style>