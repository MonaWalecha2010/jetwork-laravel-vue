<template>
    <GuestLayout>
        <Head title="Email Verification"/>

        <div class="mb-4 text-sm text-gray-600">
            Thanks for signing up! Before getting started, could you verify your email address by clicking on the link
            we just emailed to you? If you didn't receive the email, we will gladly send you another.
        </div>

        <div v-if="verificationLinkSent" class="mb-4 font-medium text-sm text-green-600">
            A new verification link has been sent to the email address you provided during registration.
        </div>

        <form @submit.prevent="submit">
            <div class="mt-4 flex items-center justify-between">
                <PrimaryButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Resend Verification Email
                </PrimaryButton>

                <Link
                    :href="route('logout')"
                    as="button"
                    class="underline text-sm text-gray-600 capitalize"
                    method="post"
                >Log Out
                </Link
                >
            </div>
        </form>
    </GuestLayout>
</template>
<script setup>
import {computed, onMounted, onUnmounted} from 'vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import {useForm} from '@inertiajs/inertia-vue3';

const props = defineProps({
    status: String,
});

const form = useForm();

const submit = () => {
    form.post(route('verification.send'));
};

const verificationLinkSent = computed(() => props.status === 'verification-link-sent');

onMounted(() => {
    document.body.classList.add('authentication');
});

onUnmounted(() => {
    document.body.classList.remove('authentication');
});
</script>
