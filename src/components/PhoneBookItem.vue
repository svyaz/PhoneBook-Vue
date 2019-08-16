<template>
    <div class="row list-element">
        <div class="col-1"><label><input type="checkbox"></label></div>
        <div class="col-1" v-text="index+1"></div>
        <div class="col-5" v-text="item.fullName"></div>
        <div class="col-4" v-text="item.phoneNumber"></div>
        <div class="col-1">
            <button title="Удалить" v-on:click="remove">x</button>
        </div>
    </div>
</template>

<script>
    export default {
        name: "PhoneBookItem",
        props: {
            item: {
                type: Object,
                required: true
            },
            index: {
                type: Number,
                required: true
            }
        },
        methods: {
            remove () {
                this.$emit("remove-item", this.item);
            }
        }
    }
</script>
