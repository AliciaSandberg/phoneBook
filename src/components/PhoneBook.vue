<template>
    <div>
        <p>PhoneBook</p>
        <button @click="currentList = 'friends'">Friends</button>
        <button @click="currentList = 'colleagues'" >Colleagues</button>
        <phone-book-table v-model="currentContact" v-if="currentList === 'colleagues'" :contacts="colleagues"/>
        <phone-book-table v-model="currentContact" v-if="currentList === 'friends'" :contacts="friends"/>
         <add :contact="currentContact" v-model="newContact" />
    </div>
</template>
<script>
import data from '../assets/phoneBook.json'
import PhoneBookTable from '../components/PhonebookTable'
import Add from '../components/Add'

export default {
  name: 'PhoneBook',
  components:{
      PhoneBookTable,
      Add
  },
  data() {
    return {
        phoneBookData: data,
        friends: [],
        colleagues: [],
        currentList: '',
        currentContact: {},
        newContact: ''
    }
  },
  /* watch: {
    newContact: function () {
       this.phoneBookData.push(this.newContact)
       this.updateLists
       return this.newContact
    }
  }, */
  methods: {
      updateLists(){
          this.phoneBookData.map(contact => {
        if(contact.company === 'BLUPLANET'){
            this.colleagues.push(contact)
        }else{
             this.friends.push(contact)
        }
     
      })
      }
  },
  mounted() {
      this.updateLists()
      
  }
}
</script>

<style lang="scss" scoped>

</style>
