<script setup>
import { useTemplateRef, onMounted } from 'vue';
import { useForm } from '@inertiajs/vue3';
import GuestAuthLayout from '@/layouts/GuestAuthLayout.vue';

const registerForm = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});

const nameInput = useTemplateRef('name-input');

const submit = () => {
    registerForm.post(route('register'), {
        onFinish: () => registerForm.reset('password', 'password_confirmation'),
    });
};

onMounted(() => {
    nameInput.value.$el.focus();
});
</script>

<template>
    <GuestAuthLayout>
        <InertiaHead title="Cadastrar" />

        <template #title>
            <div class="text-center">Criar uma conta</div>
        </template>

        <template #subtitle>
            <div class="text-center">
                Digite seus dados abaixo para criar sua conta
            </div>
        </template>

        <form class="space-y-6 sm:space-y-8" @submit.prevent="submit">
            <div class="flex flex-col gap-2">
                <label for="name">Nome</label>
                <InputText
                    id="name"
                    ref="name-input"
                    v-model="registerForm.name"
                    :invalid="Boolean(registerForm.errors?.name)"
                    type="text"
                    autocomplete="name"
                    required
                    fluid
                />
                <Message
                    v-if="registerForm.errors?.name"
                    severity="error"
                    variant="simple"
                    size="small"
                >
                    {{ registerForm.errors?.name }}
                </Message>
            </div>

            <div class="flex flex-col gap-2">
                <label for="email">Endereço de e-mail</label>
                <InputText
                    id="email"
                    v-model="registerForm.email"
                    :invalid="Boolean(registerForm.errors?.email)"
                    type="email"
                    autocomplete="username"
                    required
                    fluid
                />
                <Message
                    v-if="registerForm.errors?.email"
                    severity="error"
                    variant="simple"
                    size="small"
                >
                    {{ registerForm.errors?.email }}
                </Message>
            </div>

            <div class="flex flex-col gap-2">
                <label for="password">Senha</label>
                <Password
                    v-model="registerForm.password"
                    :invalid="Boolean(registerForm.errors?.password)"
                    autocomplete="new-password"
                    inputId="password"
                    toggleMask
                    required
                    fluid
                />
                <Message
                    v-if="registerForm.errors?.password"
                    severity="error"
                    variant="simple"
                    size="small"
                >
                    {{ registerForm.errors?.password }}
                </Message>
            </div>

            <div class="flex flex-col gap-2">
                <label for="password-confirmation">Confirmar senha</label>
                <Password
                    v-model="registerForm.password_confirmation"
                    :invalid="
                        Boolean(registerForm.errors?.password_confirmation)
                    "
                    :feedback="false"
                    autocomplete="new-password"
                    inputId="password-confirmation"
                    toggleMask
                    required
                    fluid
                />
                <Message
                    v-if="registerForm.errors?.password_confirmation"
                    severity="error"
                    variant="simple"
                    size="small"
                >
                    {{ registerForm.errors?.password_confirmation }}
                </Message>
            </div>

            <div>
                <Button
                    type="submit"
                    :loading="registerForm.processing"
                    label="Criar conta"
                    fluid
                />
            </div>

            <div class="text-center">
                <span class="text-muted-color mr-1">Já tem uma conta?</span>
                <InertiaLink :href="route('login')">
                    <Button class="p-0" variant="link" label="Entrar" />
                </InertiaLink>
            </div>
        </form>
    </GuestAuthLayout>
</template>
