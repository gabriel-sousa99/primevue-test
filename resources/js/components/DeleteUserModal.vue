<script setup>
import { useTemplateRef } from 'vue';
import { useForm } from '@inertiajs/vue3';

const modalOpen = defineModel(false, {
    type: Boolean,
});

const passwordInput = useTemplateRef('password-input');

const form = useForm({
    password: '',
});

const deleteUser = () => {
    form.delete(route('profile.destroy'), {
        preserveScroll: true,
        onSuccess: () => (modalOpen.value = false),
        onError: () => {
            const passwordInputElement =
                passwordInput.value.$el.querySelector('input');
            if (passwordInputElement) {
                passwordInputElement.focus();
            }
        },
        onFinish: () => form.reset(),
    });
};
</script>

<template>
    <Dialog
        v-model:visible="modalOpen"
        class="w-[40rem]"
        position="center"
        header="Tem certeza de que deseja excluir sua conta?"
        :draggable="false"
        dismissableMask
        modal
    >
        <div class="mb-6">
            <p class="m-0 text-muted-color">
                Uma vez que sua conta for excluída, todos os seus recursos e
                dados serão permanentemente deletados. Digite sua senha para
                confirmar que deseja excluir permanentemente sua conta.
            </p>
        </div>

        <div class="flex flex-col gap-2">
            <Password
                ref="password-input"
                v-model="form.password"
                :invalid="Boolean(form.errors?.password)"
                :feedback="false"
                autocomplete="current-password"
                inputId="password"
                toggleMask
                autofocus
                required
                fluid
                @keyup.enter="deleteUser"
            />
            <Message
                v-if="form.errors?.password"
                severity="error"
                variant="simple"
                size="small"
            >
                {{ form.errors?.password }}
            </Message>
        </div>

        <template #footer>
            <Button
                class="mr-2"
                label="Cancelar"
                plain
                text
                @click="modalOpen = false"
            />
            <Button
                :loading="form.processing"
                label="Excluir conta"
                severity="danger"
                @click="deleteUser"
            />
        </template>
    </Dialog>
</template>
