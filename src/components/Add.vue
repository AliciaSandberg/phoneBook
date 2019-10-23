<template>
    <div>
        <button @click="add = true">add</button>
         <button @click="add = false">edit/remove</button>
        {{test}}
        <div v-if="!add">
            <p>
                Edit phonebook
            </p>
            <input placeholder="namn" v-model="contact.name">
            <input placeholder="company" v-model="contact.company">
            <input placeholder="phone" v-model="contact.phone">
        </div>
         <div v-if="add">
        <p>Add</p>
        <input placeholder="namn" v-model="newContact.name">
        <input placeholder="company" v-model="newContact.company">
        <input placeholder="phone" v-model="newContact.phone">
        <button @click="addContact">Add</button>
         </div>
    </div>
</template>
<script>
export default {
    name: 'PhoneBook',
    props: {
        contact: {
            type: Object,
            required: true
        }
    },
    data() {
        return{
            newContact: {
                name: '',
                company: '',
                phone: '',
                id: ''
            },
            test: '',
            add: false
        }
    },
    methods: {
        addContact(){
            this.newContact.id = '898192898'
            this.test = this.newContact
            this.$emit('input', this.newContact)
        }
    }
}
</script>