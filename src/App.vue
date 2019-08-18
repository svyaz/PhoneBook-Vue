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

<style>
    body {
        background-color: #f0f0f0;
        font-family: Tahoma, Arial, serif;
        font-size: 14px;
        color: #222;
    }

    .top-space {
        padding-top: 1em;
    }

    .row div {
        padding-right: 10px;
        padding-left: 10px;
    }

    .row label,
    .row input,
    .row button {
        width: 100%;
    }

    .row input,
    .row button {
        border: solid 1px #bababa;
        border-radius: 3px;
    }

    .row button {
        background: linear-gradient(0deg, #cccccc, #fefefe);
    }

    .list-header {
        text-align: left;
        background-color: #87cefa;
        padding: 0.3em 0 0;
    }

    .centered {
        text-align: center;
    }

    .list-element {
        padding-top: 0.3em;
        border-bottom: solid 1px #87cefa;
    }

    .empty-field {
        background-color: #fddfdf;
    }

    .error-message {
        color: #f00;
    }

    .fade-enter-active, .fade-leave-active {
        transition: opacity 0.5s;
    }
    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
</style>
