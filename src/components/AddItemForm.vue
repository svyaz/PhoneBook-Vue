<template>
    <div>
        <div class="row top-space">
            <div class="col">
                <h5>Добавить контакт</h5>
            </div>
        </div>
        <div class="row">
            <div class="col-6 col-md-4 col-lg-3">
                <label><input type="text" placeholder="Имя" tabindex="1"
                              v-model="newFirstName"
                              :class="(isHighlighted && newFirstName === '') ? 'empty-field' : ''"></label>
            </div>
            <div class="col-6 col-md-4 col-lg-3">
                <label><input type="text" placeholder="Фамилия" tabindex="2"
                              v-model="newLastName"
                              :class="(isHighlighted && newLastName === '') ? 'empty-field' : ''"></label>
            </div>
            <div class="col-6 col-md-4 col-lg-3">
                <label><input type="text" placeholder="Телефон" tabindex="3"
                              v-model="newPhoneNumber"
                              :class="(isHighlighted && newPhoneNumber === '') ? 'empty-field' : ''"></label>
            </div>
            <div class="col-3 col-md-2">
                <button @click="addContact" tabindex="4">Добавить</button>
            </div>
        </div>
        <div class="row" v-if="isHighlighted">
            <div class="col centered">
                <span v-text="errorMessage" class="error-message"></span>
            </div>
        </div>
    </div>
</template>

<script>
    const ERR_MSG_EMPTY_ITEM_TEXT = "Нужно заполнить все поля.";

    export default {
        name: "AddItemForm",

        data() {
            return {
                newContact: {},
                newFirstName: "",
                newLastName: "",
                newPhoneNumber: "",
                isHighlighted: false,
                errorMessage: ""
            }
        },

        methods: {
            addContact() {
                if (this.newFirstName === "" || this.newLastName === "" || this.newPhoneNumber === "") {
                    this.isHighlighted = true;
                    this.errorMessage = ERR_MSG_EMPTY_ITEM_TEXT;
                    return;
                }
                this.newContact = {
                    id: (new Date()).getTime(),
                    firstName: this.newFirstName,
                    lastName: this.newLastName,
                    fullName: this.newFirstName + " " + this.newLastName,
                    phoneNumber: this.newPhoneNumber
                };
                this.newFirstName = "";
                this.newLastName = "";
                this.newPhoneNumber = "";
                this.isHighlighted = false;

                this.$emit("add-item", this.newContact);
            }
        }
    }
</script>
