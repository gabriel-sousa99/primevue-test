<script setup>
import { useTemplateRef, onMounted } from 'vue';
import { useForm } from '@inertiajs/vue3';
import GuestAuthLayout from '@/layouts/GuestAuthLayout.vue';

defineProps({
    status: {
        type: String,
    },
});

const emailInput = useTemplateRef('email-input');

const forgotPasswordForm = useForm({
    email: '',
});

const submit = () => {
    forgotPasswordForm.post(route('password.email'));
};

onMounted(() => {
    emailInput.value.$el.focus();
});
</script>

<template>
    <GuestAuthLayout>
        <InertiaHead title="Esqueci a senha" />

        <template v-if="status" #message>
            <Message severity="success" :closable="false" class="shadow-sm">
                {{ status }}
            </Message>
        </template>

        <template #title>
            <div class="text-center">Esqueci a senha</div>
        </template>

        <template #subtitle>
            <div class="text-center">
                Digite seu endereço de e-mail para receber um link de
                redefinição de senha
            </div>
        </template>

        <form class="space-y-6 sm:space-y-8" @submit.prevent="submit">
            <div class="flex flex-col gap-2">
                <label for="email">Endereço de e-mail</label>
                <InputText
                    id="email"
                    ref="email-input"
                    v-model="forgotPasswordForm.email"
                    :invalid="Boolean(forgotPasswordForm.errors?.email)"
                    type="email"
                    autocomplete="username"
                    required
                    fluid
                />
                <Message
                    v-if="forgotPasswordForm.errors?.email"
                    severity="error"
                    variant="simple"
                    size="small"
                >
                    {{ forgotPasswordForm.errors?.email }}
                </Message>
            </div>

            <div>
                <Button
                    :loading="forgotPasswordForm.processing"
                    type="submit"
                    label="Enviar link de redefinição por e-mail"
                    fluid
                />
            </div>

            <div class="text-center">
                <span class="text-muted-color mr-1">Ou, voltar para</span>
                <InertiaLink :href="route('login')">
                    <Button class="p-0" variant="link" label="entrar" />
                </InertiaLink>
            </div>
        </form>
    </GuestAuthLayout>
</template>
