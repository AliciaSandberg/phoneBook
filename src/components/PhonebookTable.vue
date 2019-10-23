<template>
    <div>
        <table>
            <tr>
            <th>Namn</th>
            <th>Category</th>
            <th>Phonenumber</th>
            </tr>
            <div
            v-for="contact in contacts" 
            :key="contact.id"
            >
                <tr @click="setCurrentContact(contact)">
                    <td>{{contact.name}}</td>
                    <td>{{contact.company}}</td>
                    <td>{{contact.phone}}</td>
                </tr>
            </div>
        </table>
    </div>
</template>

<script>

export default {
  name: 'PhoneBook',
  components: {
 
  },
  props: {
    contacts: {
      type: Array,
      required: true
    },
  },
  data() {
    return {

    }
  },
  methods: {
      setCurrentContact(contact){
         this.$emit('input', contact)
      }
  }
 
}
</script>

<style lang="scss" scoped>

</style>
