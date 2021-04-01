<template>
  <div>
    <v-row>
      <v-col :lg="8" :sm="12">
        <contacts-table :contacts="contacts" />
      </v-col>
      <v-col :lg="4" :sm="12">
        <contact-form @contact-submit="addContact" />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import ContactForm from "./ContactForm";
import ContactsTable from "./ContactsTable";

export default {
  components: { ContactForm, ContactsTable },
  data() {
    return {
      contacts: []
    };
  },
  methods: {
    addContact(newContact) {
      this.contacts.push(newContact);

      localStorage.setItem("contacts", JSON.stringify(this.contacts));
    }
  },
  mounted() {
    const existingContacts = JSON.parse(localStorage.getItem("contacts"));
    this.contacts = existingContacts || [];
  }
};
</script>

<style></style>
