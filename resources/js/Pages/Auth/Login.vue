<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

defineProps({
    canResetPassword: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const form = useForm({
    email: '',
    password: '',
    remember: false,
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />

        <!-- Background wrapper with dark overlay -->
        
            <!-- Your custom logo -->
                <div class="flex items-center">
                    <Link :href="route('dashboard')">
                        <img src="/images/new-logo.png" alt="Logo" class="h-10" />
                    </Link>
                </div>


        <div
            class="min-h-screen bg-cover bg-center relative flex items-center justify-center"
            style="background-image: url('/images/login-bg.jpg');"
        >


            <!-- Form container -->
            <div
                class="relative z-10 bg-opacity-90 rounded-lg shadow-lg p-8 max-w-md w-full "
            >
                <!-- Status message -->
                <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
                    {{ status }}
                </div>

                 <h2 class="text-3xl font-bold text-center text-[#4E342E] mb-2">WELCOME BACK </h2>
                <p class="text-sm text-center text-[#6D4C41] mb-6">Please fill in your details...</p>

                <form @submit.prevent="submit" class="space-y-6">
                    <div>
                        <InputLabel for="email" value="Email" />

                        <TextInput
                            id="email"
                            type="email"
                            class="mt-1 block w-full"
                            v-model="form.email"
                            required
                            autofocus
                            autocomplete="username"
                        />

                        <InputError class="mt-2" :message="form.errors.email" />
                    </div>

                    <div>
                        <InputLabel for="password" value="Password" />

                        <TextInput
                            id="password"
                            type="password"
                            class="mt-1"
                            v-model="form.password"
                            required
                            autocomplete="current-password"
                        />

                        <InputError class="mt-2" :message="form.errors.password" />
                    </div>

                    <div class="flex items-center">
                        <Checkbox name="remember" v-model:checked="form.remember" />
                        <label for="remember" class="ml-2 text-sm text-white">Remember me</label>
                    </div>

                    <div class="flex items-center justify-between">
                        <Link
                            v-if="canResetPassword"
                            :href="route('password.request')"
                            class="bg-gradient-to-r from-purple-600 to-pink-500 bg-clip-text text-transparent hover:from-pink-500 hover:to-purple-600 transition duration-300 ease-in-out underline"
                        >
                            Forgot your password?
                        </Link>

                        <PrimaryButton
                            :class="{ 'opacity-50 cursor-not-allowed': form.processing }"
                            :disabled="form.processing"
                        >
                            Log in
                        </PrimaryButton>
                    </div>
                </form>
            </div>
        </div>
    </GuestLayout>
</template>
