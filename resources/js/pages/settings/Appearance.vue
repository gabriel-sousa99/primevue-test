<script setup>
import AppLayout from '@/layouts/AppLayout.vue';
import SettingsLayout from '@/layouts/UserSettingsLayout.vue';
import SelectColorModeButton from '@/components/SelectColorModeButton.vue';

const breadcrumbs = [
    { label: 'Painel', route: route('dashboard') },
    { label: 'Configurações de aparência' },
];
</script>

<template>
    <AppLayout :breadcrumbs="breadcrumbs">
        <InertiaHead title="Configurações de aparência" />

        <SettingsLayout>
            <Card
                pt:body:class="max-w-2xl space-y-3"
                pt:caption:class="space-y-1"
            >
                <template #title> Configurações de aparência </template>
                <template #subtitle>
                    Atualize as configurações de aparência da sua conta
                </template>
                <template #content>
                    <SelectColorModeButton id="color-mode-selector" />
                </template>
            </Card>
        </SettingsLayout>
    </AppLayout>
</template>
