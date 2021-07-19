<template>
    <label class="section--select--multiple"
           :title="title"
           :for="name"
    >
        <span class="title">{{ title }}</span>
        <label class="item"
               v-for="item of collection"
               v-bind:key="item.id"
               :for="item.value"
        >
            <input class="value"
                   type="checkbox"
                   :name="name"
                   :id="item.value"
                   :checked="modelValue?.find(i => i.id === item.id)"
                   @input="e => changedModel(e, item)"
            />
            <span  class="title">{{ item.title }}</span>
        </label>
        <error-template :errors="errors" />
    </label>
</template>

<script>
    import ErrorTemplate from "./sectionComponents/ErrorTemplate";
    export default {
        name: "SectionSelectMultiple",
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
                type: Array,
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

        methods: {
            changedModel(e, item) {
                let res = this.modelValue?.find(i => item.id === i.id) ?? null;
                res !== null
                    ? this.$emit('update:modelValue', [...this.modelValue?.filter(i => i.id !== item.id)])
                    : this.$emit('update:modelValue', [...this.modelValue, item]);
            }
        }
    }
</script>

<style lang="sass" scoped>
    @import ./src/sass/_shared.sass

    .section--select--multiple
        @extend %template-action-effect
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
            border-bottom: 1px solid var(--color-line)

</style>