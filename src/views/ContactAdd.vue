<template>
    <div class="page">
        <h4>Thêm Liên hệ</h4>
        <ContactForm 
            :contact="contact" 
            @submit:contact="createContact" 
        />
        <p>{{ message }}</p>
    </div>
</template>

<script>
import ContactForm from '@/components/ContactForm.vue';
import contactService from '@/services/contact.service';

export default {
    components: {
        ContactForm,
    },
    data() {
        return {
            contact: {}, 
            message: "",
        };
    },
    methods: {
        async createContact(data) {
            try {
                await contactService.create(data);
                alert('Liên hệ được thêm thành công.');
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                console.log(error);
                this.message = "Đã xảy ra lỗi khi tạo liên hệ.";
            }
        },
    },
    created() {
        this.message = "";
    },
};
</script>