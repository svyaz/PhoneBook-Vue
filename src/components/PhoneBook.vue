<template>
    <div>
        <AddItemForm v-model="newContact" v-on:add-item="AddItem"></AddItemForm>
        <SearchForm></SearchForm>
        <div class="row list-header">
            <div class="col-1"><label><input type="checkbox" id="check-head"></label></div>
            <div class="col-1">№</div>
            <div class="col-5">Фамилия, имя</div>
            <div class="col-4">Телефон</div>
            <div class="col-1"></div>
        </div>
        <PhoneBookItem v-for="(item, index) in list"
                       v-bind:item="item"
                       v-bind:index="index"
                       v-bind:key="item.id"
                       v-on:remove-item="removeItem"></PhoneBookItem>
        <div class="row top-space" v-if="list.length === 0">
            <div class="col centered">Пока нет ни одного контакта.</div>
        </div>
    </div>
</template>

<script>
    import PhoneBookItem from './PhoneBookItem.vue';
    import AddItemForm from "./AddItemForm.vue";
    import SearchForm from "./SearchForm.vue";

    export default {
        name: "PhoneBook",

        components: {AddItemForm, SearchForm, PhoneBookItem},

        props: ["item"],

        data() {
            return {
                newContact: {},
                list: [],
            };
        },

        methods: {
            AddItem(item) {
                var isFound = this.list.some(function (contact) {
                    return contact.phoneNumber === item.phoneNumber;
                });

                if (isFound) {
                    this.$bvModal.msgBoxOk('Контакт с таким номером телефона уже есть!', {
                        size: 'md',
                        buttonSize: 'sm',
                        okVariant: 'primary',
                        hideHeader: true,
                        hideHeaderClose: true,
                        footerClass: 'p-2',
                        centered: false
                    });
                } else {
                    this.list.push(item);
                }
            },
            removeItem(item) {
                this.$bvModal.msgBoxConfirm('Вы действительно хотите удалить ' + item.fullName + "?", {
                    size: 'md',
                    buttonSize: 'sm',
                    okVariant: 'primary',
                    okTitle: 'Удалить',
                    cancelTitle: 'Отмена',
                    footerClass: 'p-2',
                    hideHeader: true,
                    hideHeaderClose: true,
                    centered: false
                }).then(value => {
                    if (value) {
                        this.list = this.list.filter(function (e) {
                            return e.id !== item.id;
                        });
                    }
                });
            }
        }
    }
</script>
