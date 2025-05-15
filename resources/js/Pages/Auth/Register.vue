<script setup>
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
  <GuestLayout>
    <Head title="Register" />

    <div
      class="max-w-md mx-auto p-8 rounded-lg shadow-lg"
      style="background-image: url('/images/login-bg.jpg'); background-size: cover; background-position: center;"
    >
      <h2 class="text-3xl font-bold text-center text-[#4E342E] mb-2">Create Your Account </h2>
      <p class="text-sm text-center text-[#6D4C41] mb-6">Please fill in your details to register</p>

      <form @submit.prevent="submit" class="space-y-5 text-[#4E342E] bg-white bg-opacity-80 p-6 rounded-lg">
        <div>
          <InputLabel for="name" value="Name" class="text-[#4E342E]" />
          <TextInput
            id="name"
            type="text"
            class="mt-1 block w-full rounded-lg border-[#A1887F] bg-[#FFF8F2] text-[#4E342E] focus:ring-[#8D6E63] focus:border-[#8D6E63]"
            v-model="form.name"
            required
            autofocus
            autocomplete="name"
          />
          <InputError class="mt-2" :message="form.errors.name" />
        </div>

        <div>
          <InputLabel for="email" value="Email" class="text-[#4E342E]" />
          <TextInput
            id="email"
            type="email"
            class="mt-1 block w-full rounded-lg border-[#A1887F] bg-[#FFF8F2] text-[#4E342E] focus:ring-[#8D6E63] focus:border-[#8D6E63]"
            v-model="form.email"
            required
            autocomplete="username"
          />
          <InputError class="mt-2" :message="form.errors.email" />
        </div>

        <div>
          <InputLabel for="password" value="Password" class="text-[#4E342E]" />
          <TextInput
            id="password"
            type="password"
            class="mt-1 block w-full rounded-lg border-[#A1887F] bg-[#FFF8F2] text-[#4E342E] focus:ring-[#8D6E63] focus:border-[#8D6E63]"
            v-model="form.password"
            required
            autocomplete="new-password"
          />
          <InputError class="mt-2" :message="form.errors.password" />
        </div>

        <div>
          <InputLabel for="password_confirmation" value="Confirm Password" class="text-[#4E342E]" />
          <TextInput
            id="password_confirmation"
            type="password"
            class="mt-1 block w-full rounded-lg border-[#A1887F] bg-[#FFF8F2] text-[#4E342E] focus:ring-[#8D6E63] focus:border-[#8D6E63]"
            v-model="form.password_confirmation"
            required
            autocomplete="new-password"
          />
          <InputError class="mt-2" :message="form.errors.password_confirmation" />
        </div>

        <div class="flex items-center justify-between text-sm mt-2">
        <Link
            :href="route('login')"
            class="bg-gradient-to-r from-purple-600 to-pink-500 bg-clip-text text-transparent hover:from-pink-500 hover:to-purple-600 transition duration-300 ease-in-out underline"
        >
            Already registered?
        </Link>
        </div>


        <button
        type="submit"
        class="w-full bg-gradient-to-r from-purple-600 to-pink-500 hover:from-pink-500 hover:to-purple-600 text-white font-semibold py-3 rounded-xl shadow-md transition-all duration-300 ease-in-out"
        :class="{ 'opacity-25': form.processing }"
        :disabled="form.processing"
        >
        Register
        </button>

      </form>
    </div>
  </GuestLayout>
</template>