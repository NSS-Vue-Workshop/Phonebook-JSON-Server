<template>
  <div>
    <h3 class="teal--text">New Contact</h3>
    <v-form id="contact-form" @submit.prevent="handleSubmit" ref="contactForm">
      <v-text-field
        id="firstName"
        :rules="validators.firstName"
        outlined
        label="First Name"
        v-model="form.firstName"
      />
      <v-text-field
        id="lastName"
        outlined
        label="Last Name"
        v-model="form.lastName"
      />
      <v-text-field
        id="phone"
        type="text"
        outlined
        label="Phone"
        v-model="form.phone"
      />
      <v-select
        id="phoneType"
        outlined
        label="Phone Type"
        :items="phoneTypeOptions"
        v-model="form.type"
      />
      <v-text-field id="email" outlined label="Email" v-model="form.email" />
      <v-btn class="form-submit" type="submit" color="teal" dark>Submit</v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        firstName: "",
        lastName: "",
        phone: "",
        type: "",
        email: ""
      },
      phoneTypeOptions: ["Home", "Cell", "Office"],
      validators: {
        firstName: [
          val => !!val || "Contact first name is required",
          val => val.length < 25 || "First name must be less than 25 characters"
        ]
      }
    };
  },
  methods: {
    handleSubmit() {
      const isValid = this.$refs.contactForm.validate();
      if (!isValid) return;

      this.$emit("contact-submit", this.form);

      this.form = {
        firstName: "",
        lastName: "",
        phone: "",
        type: "",
        email: ""
      };
      this.$refs.contactForm.resetValidation();
    }
  }
};
</script>

<style></style>
