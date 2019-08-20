<template>
    <div id="app" class="container">
        <div class="row top-space">
            <div class="col">
                <h3>Контакты</h3>
            </div>
        </div>
        <PhoneBook></PhoneBook>
    </div>
</template>

<script>
    import PhoneBook from './components/PhoneBook.vue';

    export default {
        name: 'app',
        components: {
            PhoneBook
        }
    }
</script>

<style lang="sass">
    $font: Tahoma, Arial, serif
    $fontSize: 14px
    $grey: #f0f0f0
    $grey1: #bababa
    $grey2: #cccccc
    $grey3: #fefefe
    $almostBlack: #222
    $lightPink: #fddfdf
    $red: #f00
    $padding: 10px
    $paddingInput: 5px

    body
        background-color: $grey
        font-family: $font
        font-size: $fontSize
        color: $almostBlack

    .top-space
        padding-top: 1em

    .row div
        padding-right: $padding
        padding-left: $padding

    .row label,
    .row input,
    .row button
        width: 100%

    .row input,
    .row button
        border: solid 1px $grey1
        border-radius: 3px

    .row button
        background: linear-gradient(0deg, $grey2, $grey3)

    .row input
        padding-left: $paddingInput
        padding-right: $paddingInput

    .centered
        text-align: center

    .empty-field
        background-color: $lightPink

    .error-message
        color: $red

    .fade-enter-active,
    .fade-leave-active
        transition: opacity 0.5s

    .fade-enter,
    .fade-leave-to
        opacity: 0
</style>
