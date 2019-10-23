<template>
    <div>
        <p>PhoneBook</p>
        <button @click="currentList = 'friends'">Friends</button>
        <button @click="currentList = 'colleagues'" >Colleagues</button>
        <phone-book-table v-model="currentContact" v-if="currentList === 'colleagues'" :contacts="colleagues"/>
        <phone-book-table v-model="currentContact" v-if="currentList === 'friends'" :contacts="friends"/>
       


        <button @click="AddEdit = true">add</button>
         <button @click="AddEdit = false">edit/remove</button>
   
        <div v-if="!AddEdit">
            <p>
                Edit phonebook
            </p>
            <input placeholder="namn" v-model="currentContact.name">
            <input placeholder="company" v-model="currentContact.company">
            <input placeholder="phone" v-model="currentContact.phone">
            <button @click="updateContact(currentContact)"> update</button>
            <button @click="deleteContact(currentContact)"> delete</button>
        </div>

        <div v-if="AddEdit">
        <p>Add</p>
        <input placeholder="namn" v-model="newContact.name">
        <input placeholder="company" v-model="newContact.company">
        <input placeholder="phone" v-model="newContact.phone">
        <button @click="addContact">Add</button>
         </div>
      
    </div>
</template>
<script>
import data from '../assets/phoneBook.json'
import PhoneBookTable from '../components/PhonebookTable'

export default {
  name: 'PhoneBook',
  components:{
      PhoneBookTable,
    
  },
  data() {
    return {
        AddEdit: true,
        phoneBookData: data,
        friends: [],
        colleagues: [],
        currentList: '',
        currentContact: {},
        newContact: {
                name: '',
                company: '',
                phone: '',
                id: ''
            },
    }
  },
   watch: {
    newContactList: function () {
        alert(this.newContactList)
    this.phoneBookData = this.newContactList
       this.updateLists
       return this.newContactList
    }
  }, 
  methods: {
      updateContact(contact){
           this.phoneBookData.map(c => {
               if(contact.id === c.id){
                   c = contact;
               }
           })
            this.updateLists()
      },
      deleteContact(contact){
          console.error(this.phoneBookData);
          let temp = this.phoneBookData
          let index;
         
         for(let i = 0; i < temp.length; i++){
               if(contact.id === temp[i].id){
                   index = i
               }
         }
        temp.slice(index)
        this.phoneBookData = temp
        this.updateLists()

      },
      updateLists(){
          this.friends = []
          this.colleagues = []
          this.phoneBookData.map(contact => {
        if(contact.company === 'BLUPLANET'){
            this.colleagues.push(contact)
        }else{
             this.friends.push(contact)
        }
     
      })
      },
        addContact(){
            this.newContact.id = '898192898'
            this.phoneBookData.push(this.newContact)
            this.updateLists()
        }
  },
  mounted() {
      this.updateLists()
      
  }
}
</script>

<style lang="scss" scoped>

</style>
