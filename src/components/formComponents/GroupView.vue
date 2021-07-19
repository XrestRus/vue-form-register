<template>
    <form class="group"
          action="#"
          method="post"
          @submit.prevent="e => submit(e)"
    >
        <transition name="group-animation" mode="out-in">
            <div class="group-wrap"
                 v-if="currentState.id === STATE[0].id"
            >
                <group-body>
                    <section-input name="surname"
                                   title="Фамилия*"
                                   v-model="v$.surname.$model"
                                   :errors="v$.surname.$errors"
                    />
                    <section-input name="name"
                                   title="Имя*"
                                   v-model="v$.name.$model"
                                   :errors="v$.name.$errors"
                    />
                    <section-input name="patronymic"
                                   title="Отчество"
                                   v-model="patronymic"
                    />
                </group-body>
                <group-body>
                    <section-input name="birthday"
                                   title="День рождения*"
                                   v-model="v$.birthday.$model"
                                   :errors="v$.birthday.$errors"
                                   type="date"
                    />
                    <section-input name="phone"
                                   title="Номер телефона*"
                                   v-model="v$.phone.$model"
                                   :errors="v$.phone.$errors"
                                   type="tel"
                    />
                    <section-select name="gender"
                                    title="Пол"
                                    :collection="collectionGender"
                                    v-model="gender"
                    />
                </group-body>
                <group-body>
                    <section-select name="therapist"
                                    title="Лечащий врач"
                                    :collection="collectionTherapist"
                                    v-model="therapist"
                    />

                    <section-select-multiple name="customerGroup"
                                             title="Группа клиентов*"
                                             :collection="collectionCustomerGroup"
                                             v-model="v$.customerGroup.$model"
                                             :errors="v$.customerGroup.$errors"
                    />

                    <section-check-box name="canSubmitMessage"
                                       title="Не отправлять СМС"
                                       v-model="canSubmitMessage"
                    />
                </group-body>
            </div>

            <div class="group-wrap"
                 v-else-if="currentState.id === STATE[1].id"
            >
                <group-body>
                    <section-input name="index"
                                   title="Индекс"
                                   v-model="index"
                                   type="number"
                    />
                    <section-input name="country"
                                   title="Страна"
                                   v-model="country"
                    />
                    <section-input name="region"
                                   title="Регион"
                                   v-model="region"
                    />
                </group-body>
                <group-body>
                    <section-input name="city"
                                   title="Город*"
                                   v-model="v$.city.$model"
                                   :errors="v$.city.$errors"
                    />
                    <section-input name="street"
                                   title="Улица"
                                   v-model="street"
                    />
                    <section-input name="house"
                                   title="Дом"
                                   v-model="house"
                                   type="number"
                    />
                </group-body>
            </div>

            <div class="group-wrap"
                 v-else-if="currentState.id === STATE[2].id"
            >
                <group-body>
                    <section-select name="documentType"
                                    title="Тип документа*"
                                    :collection="collectionDocumentType"
                                    v-model="v$.documentType.$model"
                                    :errors="v$.documentType.$errors"
                    />
                    <section-input name="series"
                                   title="Серия"
                                   v-model="series"
                                   type="number"
                    />
                    <section-input name="room"
                                   title="Номер"
                                   v-model="room"
                                   type="number"
                    />
                </group-body>
                <group-body>
                    <section-input name="issuedBy"
                                   title="Кем выдан"
                                   v-model="issuedBy"
                    />
                    <section-input name="dateOfIssue"
                                   title=" Дата выдачи*"
                                   v-model="v$.dateOfIssue.$model"
                                   :errors="v$.dateOfIssue.$errors"
                                   type="date"
                    />
                </group-body>
            </div>
        </transition>


        <group-bottom
            v-model="currentState"
            :states="STATE"
        />


    </form>
</template>

<script>
    import GroupBody from "./GroupBody";
    import GroupBottom from "./GroupBottom";
    import SectionInput from "./sections/SectionInput";
    import SectionSelect from "./sections/SectionSelect";
    import SectionCheckBox from "./sections/SectionCheckBox";
    import SectionSelectMultiple from "./sections/SectionSelectMultiple";
    import { STATE } from "./utilits/STATE";

    import {required, maxLength, helpers, minLength} from '@vuelidate/validators'
    import { useVuelidate } from '@vuelidate/core'
    import {REQUIREDRU, MAXLENGTHRU, MINLENGTHRU, validatorCheckFirstNumber, VCFNRU} from "./utilits/CastomValidators";

    export default {
        name: "GroupData",

        components: {
            SectionSelectMultiple,
            SectionCheckBox,
            SectionSelect,
            GroupBottom,
            GroupBody,
            SectionInput
        },

        props: {
            initState: {
                type: Object,
                default: null
            }
        },

        setup() {
            return {
                STATE,
                v$: useVuelidate()
            }
        },

        data() {
            return {

                // Тестовые данные

                collectionDocumentType: [
                    { id: 0, title: 'Паспорт' },
                    { id: 1, title: 'Свидетельство о рождении' },
                    { id: 2, title: ' Вод. удостоверение' }
                ],
                collectionCustomerGroup: [
                    { id: 0, title: 'VIP' },
                    { id: 1, title: 'Проблемный' },
                    { id: 2, title: 'ОМС' }
                ],
                collectionTherapist: [
                    { id: 0, value: 'chern', title: 'Чернышева' },
                    { id: 1, value: 'ivan', title: 'Иванов' },
                    { id: 2, value: 'zax', title: 'Захаров' }
                ],
                collectionGender: [
                    { id: 0, value: 'man', title: 'Мужской' },
                    { id: 1, value: 'woman', title: 'Женщина' }
                ],

                // Тестовый объект

                surname: 'Иванов',
                name: 'Иван',
                patronymic: 'Иваныч',
                birthday: '1977-04-29',
                phone: '79233601188',
                gender: { id: 0, value: 'man', title: 'Мужской' },
                therapist: { id: 1, value: 'ivan', title: 'Иванов' },
                customerGroup: [{ id: 1, title: 'Проблемный' }],
                canSubmitMessage: true,

                index: '6661234',
                country: 'Россия',
                region: 'Красноярск',
                city: 'Покровка',
                street: 'Промышленная',
                house: '53',

                documentType: { id: 0, title: 'Паспорт' },
                series: '0411',
                room: '232323',
                issuedBy: 'МВД ГУ Г.Ачинск',
                dateOfIssue: '2000-04-29',

                currentState: STATE[0] // USERDATA
            }
        },

        validations() {
            return {
                surname: { required: helpers.withMessage(REQUIREDRU, required) },
                name: { required: helpers.withMessage(REQUIREDRU, required) },
                birthday: { required: helpers.withMessage(REQUIREDRU, required) },
                phone: {
                    required: helpers.withMessage(REQUIREDRU, required),
                    maxLength: helpers.withMessage(MAXLENGTHRU, maxLength(11)),
                    minLength: helpers.withMessage(MINLENGTHRU, minLength(11)),
                    validatorCheckFirstNumber: helpers.withMessage(VCFNRU, validatorCheckFirstNumber)
                },
                customerGroup: { required: helpers.withMessage(REQUIREDRU, required) },

                city: { required: helpers.withMessage(REQUIREDRU, required) },

                documentType: { required: helpers.withMessage(REQUIREDRU, required) },
                dateOfIssue: { required: helpers.withMessage(REQUIREDRU, required) },
            }
        },

        methods: {
            submit() {
                this.v$.$touch()
                if (this.v$.$error) {
                    alert('При заполнении формы допущены ошибки');
                } else {
                    alert('Клиент успешно создан!');
                    // Отправка
                }
            }
        }
    }
</script>

<style lang="sass">
    .group
        input
            outline: none
            border: 0

        .group-title
            display: flex
            align-items: center
            justify-content: center

            .wrap-img
                padding: 1rem
                margin: 1rem
                border-radius: 100%
                border: 2px solid #0006ff

                .img
                    height: 100px

        .group-wrap
            width: 100vw
            max-width: 800px
            min-height: 550px
            display: flex
            flex-wrap: wrap
            border-top: 1px solid var(--color-dis)
            border-bottom: 1px solid var(--color-dis)

    .group-animation
        transition: .5s

    .group-animation-enter-active
        animation: right .5s ease-out both

    .group-animation-leave-active
        animation: left .5s ease-out both

    @keyframes left
        0%
            transform: translateX(0px)
            opacity: 1

        100%
            transform: translateX(-200px)
            opacity: 0

    @keyframes right
        0%
            transform: translateX(200px)
            opacity: 0

        100%
            transform: translateX(0px)
            opacity: 1
</style>