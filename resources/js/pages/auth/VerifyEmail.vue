<script setup>
import { computed } from 'vue';
import { useForm } from '@inertiajs/vue3';
import GuestAuthLayout from '@/layouts/GuestAuthLayout.vue';

const props = defineProps({
    status: {
        type: String,
    },
});

const sendVerificationForm = useForm({});
const submit = () => {
    sendVerificationForm.post(route('verification.send'));
};
const logoutForm = useForm({});
const logout = () => {
    logoutForm.post(route('logout'));
};

const verificationLinkSent = computed(
    () => props.status === 'verification-link-sent'
);
</script>

<template>
    <GuestAuthLayout>
        <InertiaHead title="Verificação de e-mail" />

        <template #title>
            <div class="text-center">Verificar e-mail</div>
        </template>

        <template #subtitle>
            <div class="text-center">
                Verifique seu endereço de e-mail clicando no link que acabamos
                de enviar para você.
            </div>
        </template>

        <template v-if="verificationLinkSent" #message>
            <Message severity="success" :closable="false" class="shadow-sm">
                Um novo link de verificação foi enviado para o endereço de
                e-mail que você forneceu durante o cadastro.
            </Message>
        </template>

        <div class="space-y-6 sm:space-y-8">
            <form @submit.prevent="submit">
                <Button
                    :loading="sendVerificationForm.processing"
                    type="submit"
                    label="Reenviar e-mail de verificação"
                    fluid
                />
            </form>
            <div class="text-center">
                <Button
                    :loading="logoutForm.processing"
                    class="p-0"
                    variant="link"
                    label="Sair"
                    @click="logout"
                />
            </div>
        </div>
    </GuestAuthLayout>
</template>
