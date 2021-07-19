<template>
    <label class="section--select"
           :title="title"
           :for="name"
    >
        <span class="title">{{ title }}</span>
        <select class="item"
                :name="name"
                :id="name"
                @input="e => $emit('update:modelValue', JSON.parse(e.target.value))"
        >
            <option v-for="item in collection"
                    v-bind:key="item.id"
                    :value="JSON.stringify(item)"
                    :selected="item.id === modelValue.id"
            >
                {{ item.title }}
            </option>
        </select>
        <error-template :errors="errors" />
    </label>
</template>

<script>
    import ErrorTemplate from "./sectionComponents/ErrorTemplate";
    export default {
        name: "SectionSelect",
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
            collection: {
                type: Array,
                default: null
            },
            modelValue: {
                type: Object,
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

    .section--select
        display: flex
        flex-direction: column
        margin: 1rem 0

        &>.title,
        .item,
        .item .title
            @extend %template-section-item

        &>.title
            border-bottom: 1px solid var(--color-line)

        .item
            @extend %template-action-effect
            border: 0
            border-bottom: 1px solid var(--color-line)
            outline: none

</style>