<script setup>
import AppLayout from '@/layouts/AppLayout.vue';

const breadcrumbs = [{ label: 'Painel' }];
</script>

<template>
    <AppLayout :breadcrumbs="breadcrumbs">
        <InertiaHead title="Painel" />

        <Card>
            <template #content>
                <p class="m-0">Você está logado!</p>
            </template>
        </Card>
    </AppLayout>
</template>
