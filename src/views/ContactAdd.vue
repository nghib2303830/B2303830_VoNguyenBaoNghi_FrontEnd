<template>
    <div class="page">
        <h4>Thêm liên hệ mới</h4>
        <ContactForm :contact="contact" @submit:contact="addContact" />
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
    data() {
        return {
            contact: null,
            message: "",
        };
    },
    methods: {
        async addContact(data) {
            try {
                await ContactService.create(data);
                alert("Thêm liên hệ mới thành công");
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
            }
        },
    },
    created() {
        this.contact = {
            name: "",
            email: "",
            address: "",
            phone: "",
            favorite: false,
        };
        this.message = "";
    },
}
</script>