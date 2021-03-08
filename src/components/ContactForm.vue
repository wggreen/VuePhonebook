<template>
  <div>
    <h3 class="teal--text">New Contact</h3>
    <v-form @submit.prevent="handleSubmit" ref="contactForm">
      <v-text-field
        outlined
        label="First Name"
        v-model="form.firstName"
        :rules="validators.firstName"
      />
      <v-text-field
        outlined
        label="Last Name"
        v-model="form.lastName"
        :rules="validators.lastName"
      />
      <v-text-field
        type="number"
        outlined
        label="Phone"
        v-model="form.phone"
        :rules="validators.phone"
      />
      <!-- TODO: phone type -->
      <v-select
        outlined
        label="Phone Type"
        :items="phoneTypeOptions"
        v-model="form.type"
      />
      <v-text-field
        outlined
        label="Email"
        v-model="form.email"
        :rules="validators.email"
      />
      <v-btn type="submit" color="teal" dark>Submit</v-btn>
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
        email: "",
      },
      phoneTypeOptions: ["Home", "Cell", "Office"],
      validators: {
        firstName: [
          (val) => !!val || "Contact first name is required",
          (val) =>
            val.length < 25 || "First name must be less than 25 characters",
        ],
        lastName: [
          (val) => !!val || "Contact last name is required",
          (val) =>
            val.length < 25 || "Last name must be less than 25 characters",
        ],
        phone: [
          (val) => !!val || "Contact phone number is required",
          (val) => val.length === 10 || "Phone must be exactly 10 characters",
        ],
        email: [
          (val) => !!val || "Contact email is required",
          (val) => val.includes("@") || "Email must contain @",
        ],
      },
    };
  },
  methods: {
    handleSubmit() {
      const isValid = this.$refs.contactForm.validate();
      if (!isValid) {
        // Form is not valid. Exit the method
        return;
      }

      this.$emit("contact-submit", this.form);
      this.form = {
        firstName: "",
        lastName: "",
        phone: "",
        type: "",
        email: "",
      };
      this.$refs.contactForm.resetValidation();
    },
  },
};
</script>

<style></style>