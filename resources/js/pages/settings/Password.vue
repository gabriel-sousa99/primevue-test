<script setup>
import { useTemplateRef } from 'vue';
import { useForm } from '@inertiajs/vue3';
import { useToast } from 'primevue/usetoast';
import Password from 'primevue/password';
import AppLayout from '@/layouts/AppLayout.vue';
import SettingsLayout from '@/layouts/UserSettingsLayout.vue';

defineProps({
    mustVerifyEmail: {
        type: Boolean,
    },
    status: {
        type: String,
    },
});

const breadcrumbs = [
    { label: 'Painel', route: route('dashboard') },
    { label: 'Configurações de senha' },
];

const currentPasswordInput = useTemplateRef('current-password-input');
const newPasswordInput = useTemplateRef('new-password-input');

const toast = useToast();
const updatePasswordForm = useForm({
    current_password: '',
    password: '',
    password_confirmation: '',
});

const showSuccessToast = () => {
    toast.add({
        severity: 'success',
        summary: 'Salvo',
        detail: 'Sua senha foi atualizada',
        life: 3000,
    });
};
const updatePassword = () => {
    updatePasswordForm.put(route('password.update'), {
        preserveScroll: true,
        onSuccess: () => {
            updatePasswordForm.reset();
            showSuccessToast();
        },
        onError: () => {
            if (updatePasswordForm.errors?.password) {
                updatePasswordForm.reset('password', 'password_confirmation');
                const newPasswordInputElement =
                    newPasswordInput.value.$el.querySelector('input');
                if (newPasswordInputElement) {
                    newPasswordInputElement.focus();
                }
            }
            if (updatePasswordForm.errors?.current_password) {
                updatePasswordForm.reset('current_password');
                const currentPasswordInputElement =
                    currentPasswordInput.value.$el.querySelector('input');
                if (currentPasswordInputElement) {
                    currentPasswordInputElement.focus();
                }
            }
        },
    });
};
</script>

<template>
    <AppLayout :breadcrumbs="breadcrumbs">
        <InertiaHead title="Configurações de senha" />

        <SettingsLayout>
            <Card
                pt:body:class="max-w-2xl space-y-3"
                pt:caption:class="space-y-1"
            >
                <template #title> Atualizar senha </template>
                <template #subtitle>
                    Certifique-se de que sua conta está usando uma senha longa e
                    aleatória para permanecer segura
                </template>
                <template #content>
                    <form class="space-y-6" @submit.prevent="updatePassword">
                        <div class="flex flex-col gap-2">
                            <label for="current-password">Senha atual</label>
                            <Password
                                ref="current-password-input"
                                v-model="updatePasswordForm.current_password"
                                :invalid="
                                    Boolean(
                                        updatePasswordForm.errors
                                            ?.current_password
                                    )
                                "
                                :feedback="false"
                                autocomplete="current-password"
                                inputId="current-password"
                                toggleMask
                                required
                                fluid
                            />
                            <Message
                                v-if="
                                    updatePasswordForm.errors?.current_password
                                "
                                severity="error"
                                variant="simple"
                                size="small"
                            >
                                {{
                                    updatePasswordForm.errors?.current_password
                                }}
                            </Message>
                        </div>
                        <div class="flex flex-col gap-2">
                            <label for="password">Nova senha</label>
                            <Password
                                ref="new-password-input"
                                v-model="updatePasswordForm.password"
                                :invalid="
                                    Boolean(updatePasswordForm.errors?.password)
                                "
                                autocomplete="new-password"
                                inputId="password"
                                toggleMask
                                required
                                fluid
                            />
                            <Message
                                v-if="updatePasswordForm.errors?.password"
                                severity="error"
                                variant="simple"
                                size="small"
                            >
                                {{ updatePasswordForm.errors?.password }}
                            </Message>
                        </div>
                        <div class="flex flex-col gap-2">
                            <label for="password-confirmation"
                                >Confirmar nova senha</label
                            >
                            <Password
                                v-model="
                                    updatePasswordForm.password_confirmation
                                "
                                :invalid="
                                    Boolean(
                                        updatePasswordForm.errors
                                            ?.password_confirmation
                                    )
                                "
                                :feedback="false"
                                autocomplete="confirm-password"
                                inputId="password-confirmation"
                                toggleMask
                                required
                                fluid
                            />
                            <Message
                                v-if="
                                    updatePasswordForm.errors
                                        ?.password_confirmation
                                "
                                severity="error"
                                variant="simple"
                                size="small"
                            >
                                {{
                                    updatePasswordForm.errors
                                        ?.password_confirmation
                                }}
                            </Message>
                        </div>
                        <Button
                            :loading="updatePasswordForm.processing"
                            type="submit"
                            label="Salvar senha"
                        />
                    </form>
                </template>
            </Card>
        </SettingsLayout>
    </AppLayout>
</template>
