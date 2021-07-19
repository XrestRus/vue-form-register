<template>
    <div class="group-bottom">
        <button :disabled="canLeft"
                class="btn btn--left"
                @click="e => prevAction(e)"
                type="button"
                title="Назад"
        >
        </button>

        <div class="status">
            <div class="item"
                 v-for="item in states"
                 :key="item.id"
                 :class="{ currentItem: item.id === modelValue.id }"
                 :title="item.title"
            >
            </div>
        </div>

        <button v-if="!canRight"
                :disabled="canRight"
                class="btn btn--right"
                @click="e => nextAction(e)"
                type="button"
                title="Вперед"
        >
        </button>
        <button v-else-if="canRight"
                class="btn btn--submit"
                type="submit"
                title="Отправит"
        >
        </button>

    </div>
</template>

<script>
    export default {
        name: "GroupBottom",

        props: {
            modelValue: {
                type: Object,
                default: null
            },
            states: {
                type: Object,
                default: null
            }
        },

        computed: {
            canLeft: function () {
                return this.modelValue.id === 0
            },
            canRight: function () {
                return this.modelValue.id === this.states.length - 1
            }
        },

        methods: {
            prevAction: function() {
                let state = this.states.find(i => i.id === this.modelValue.id - 1) ?? this.modelValue;

                this.$emit('update:modelValue', state);
            },
            nextAction: function() {
                let state = this.states.find(i => i.id === this.modelValue.id + 1) ?? this.modelValue;

                this.$emit('update:modelValue', state);
            }
        },
    }
</script>

<style lang="sass" scoped>
    .group-bottom
        display: flex
        justify-content: center
        margin-top: .5rem
        align-items: center
        flex-wrap: wrap

        .btn
            background-color: white
            border: 1px solid var(--color-section)
            outline: 0
            border-radius: 100%
            width: 50px
            height: 50px
            cursor: pointer
            background-repeat: no-repeat
            background-position: center
            background-size: 59%
            transition: 0.4s

            &:disabled
                background-color: var(--color-dis)

            &:hover 
                box-shadow: 0 0 4px 0 var(--color-section)

        .btn--left
            background-image: url("../../assets/right-arrow.svg")
            transform: rotate(180deg)

        .btn--right
            background-image: url("../../assets/right-arrow.svg")

        .btn--submit
            background-image: url("../../assets/upload.svg")

        .status
            margin: 1rem
            display: flex

            .item
                background: transparent
                border: 1px solid var(--color-section)
                outline: 0
                border-radius: 40%
                padding: .3rem
                margin: .3rem
                position: relative
                transition: .5s

                &:not(&:nth-last-child(1))::after
                    content: ""
                    position: absolute
                    background: var(--color-section)
                    width: 10px
                    height: 1px
                    z-index: 0
                    right: -10px

            .currentItem
                box-shadow: 0 0 4px 0 var(--color-section)
                background: var(--color-section)
</style>