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
import axios from "axios";
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
    async addContact(newContact) {
      const { data } = await axios.post("/api/contacts", newContact);

      this.contacts.push(data);
    }
  },
  async mounted() {
    const { data } = await axios.get("/api/contacts");
    this.contacts = data;
  }
};
</script>

<style></style>
