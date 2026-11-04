<template>
  <div class="page">
    <h4>Thêm mới liên hệ</h4>
    <ContactForm :contact="contact" @submit:contact="create"> </ContactForm>
    <p>{{ message }}</p>
  </div>
</template>
<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";
export default {
  components: {
    ContactForm,
  },
  props: {
    id: { type: String, required: true },
  },
  data() {
    return {
      contact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
      message: "",
    };
  },
  methods: {
    async create(data) {
      try {
        this.contact = await ContactService.create(data);
        alert("Thêm liên hệ thành công.");

        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
