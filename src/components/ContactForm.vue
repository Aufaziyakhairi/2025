// ContactForm.vue
<template>
  <div class="max-w-md p-6 mx-auto shadow-2xl rounded-2xl">
    <form @submit.prevent="sendEmail" class="space-y-4">
      <div>
        <label for="name" class="block mb-2">Nama:</label>
        <input type="text" id="name" v-model="formData.name" class="w-full p-2 border rounded" required />
      </div>

      <div>
        <label for="email" class="block mb-2">Email:</label>
        <input type="email" id="email" v-model="formData.email" class="w-full p-2 border rounded" required />
      </div>

      <div>
        <label for="message" class="block mb-2">Pesan:</label>
        <textarea id="message" v-model="formData.message" class="w-full h-32 p-2 border rounded" required></textarea>
      </div>

      <button type="submit" class="w-full p-2 text-white duration-700 bg-green-500 rounded hover:text-black hover:bg-white" :disabled="loading">
        {{ loading ? 'Mengirim...' : 'Kirim Pesan' }}
      </button>
    </form>
  </div>
</template>

<script>
import emailjs from '@emailjs/browser';

export default {
  name: 'ContactForm',
  data() {
    return {
      formData: {
        name: '',
        email: '',
        message: ''
      },
      loading: false
    }
  },
  methods: {
    async sendEmail() {
      try {
        this.loading = true;

        const templateParams = {
          from_name: this.formData.name,
          from_email: this.formData.email,
          message: this.formData.message,
        };

        await emailjs.send(
          'service_huo41o8', // Ganti dengan Service ID Anda dari EmailJS
          'template_jc83iy4', // Ganti dengan Template ID Anda
          templateParams,
          'RJS2vCsEDYS6pSz5r' // Ganti dengan Public Key Anda
        );

        alert('Pesan berhasil dikirim!');
        this.resetForm();
      } catch (error) {
        console.error('Error:', error);
        alert('Gagal mengirim pesan. Silakan coba lagi.');
      } finally {
        this.loading = false;
      }
    },
    resetForm() {
      this.formData = {
        name: '',
        email: '',
        message: ''
      };
    }
  }
}
</script>
