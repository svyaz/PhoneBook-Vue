<template>
    <div>
        <AddItemForm v-model="newContact" @add-item="addItem"></AddItemForm>
        <SearchForm @search-items="setSearchString"></SearchForm>
        <div class="row list-header">
            <div class="col-1"><label><input type="checkbox" v-model="selectAll"></label></div>
            <div class="col-1">№</div>
            <div class="col-5">Имя и фамилия</div>
            <div class="col-4">Номер телефона</div>
            <div class="col-1"></div>
        </div>
        <transition-group name="fade">
            <PhoneBookItem v-for="(item, index) in filteredList"
                           :item="item"
                           :index="index"
                           :key="item.id"
                           :selectAll="selectAll"
                           @remove-item="removeItem"
                           @selection-changed="changeItemSelection"></PhoneBookItem>
        </transition-group>
        <transition name="fade">
            <div class="row top-space" v-if="list.length === 0">
                <div class="col centered">Пока нет ни одного контакта.</div>
            </div>
        </transition>
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
                /* для изменения чекбоксов в элементах списка */
                selectAll: false,

                /* для получения нового контакта из формы добавления */
                newContact: {},

                /* для хранения списка контактов */
                list: [
                    /*{id: 1000, firstName: "John", lastName: "Lennon", fullName: "John Lennon", phoneNumber: "111-111-111"},
                    {id: 2000, firstName: "Ned", lastName: "Stark", fullName: "Ned Stark", phoneNumber: "222-222-222"},
                    {id: 3000, firstName: "Michael", lastName: "Boyarskiy", fullName: "Michael Boyarskiy", phoneNumber: "333-333-333"},
                    {id: 4000, firstName: "Max", lastName: "Kuzhelev", fullName: "Max Kuzhelev", phoneNumber: "444-444-444"}*/
                ],

                /* для хранения контактов, отмеченных чекбоксами */
                selectedList: [],

                /* для поиска */
                searchString: ""
            };
        },

        computed: {
            filteredList: function () {
                let str = this.searchString.toLowerCase();
                return this.list.filter(function (item) {
                    return (str.length === 0 ||
                        item.firstName.toLowerCase().indexOf(str) >= 0 ||
                        item.lastName.toLowerCase().indexOf(str) >= 0 ||
                        item.phoneNumber.toLowerCase().indexOf(str) >= 0);
                });
            }
        },

        methods: {
            addItem(item) {
                let isFound = this.list.some(function (contact) {
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
                let confirmMessage = this.selectedList.length === 0 ?
                    `Вы действительно хотите удалить ${item.fullName}?` :
                    `Вы действительно хотите удалить выбранные контакты?`;

                this.$bvModal.msgBoxConfirm(confirmMessage, {
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
                        let toDelete = this.selectedList.length === 0 ?
                            [item] : this.selectedList;

                        this.list = this.list.filter(function (e) {
                            return !toDelete.includes(e);
                        });

                        this.selectedList = [];
                        this.selectAll = false;
                    }
                });
            },
            changeItemSelection(item, newValue) {
                /* Добавление/удаление из списка с установленным чекбоксом */
                if (newValue) {
                    //добавить если нет
                    if (!this.selectedList.includes(item)) {
                        this.selectedList.push(item);
                    }
                } else {
                    //удалить если есть
                    this.selectedList = this.selectedList.filter(function (e) {
                        return e.id !== item.id;
                    });
                }
            },
            setSearchString(searchString) {
                this.searchString = searchString;
            }
        }
    }
</script>
