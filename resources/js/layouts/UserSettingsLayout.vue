<script setup>
import { computed } from 'vue';
import { usePage } from '@inertiajs/vue3';

const page = usePage();
const currentRoute = computed(() => {
    // Access page.url to trigger re-computation on navigation.
    /* eslint-disable @typescript-eslint/no-unused-vars */
    const url = page.url;
    /* eslint-enable @typescript-eslint/no-unused-vars */
    return route().current();
});

const sidebarNavItems = computed(() => [
    {
        title: 'Perfil',
        route: route('profile.edit'),
        active: currentRoute.value == 'profile.edit',
    },
    {
        title: 'Senha',
        route: route('password.edit'),
        active: currentRoute.value == 'password.edit',
    },
    {
        title: 'Aparência',
        route: route('appearance'),
        active: currentRoute.value == 'appearance',
    },
]);
</script>

<template>
    <div>
        <PageTitleSection>
            <template #title> Configurações </template>
            <template #subTitle>
                Gerencie suas configurações de perfil e conta
            </template>
        </PageTitleSection>

        <Divider class="my-8" />

        <div class="flex flex-col gap-6 lg:gap-8 lg:flex-row">
            <aside class="w-full md:max-w-2xl lg:w-48">
                <nav class="flex flex-col space-x-0 space-y-1">
                    <Button
                        v-for="item in sidebarNavItems"
                        :key="item.route"
                        pt:root:class="flex items-center justify-start no-underline"
                        :severity="item.active ? 'secondary' : ''"
                        :variant="item.active ? 'outlined' : 'text'"
                        :href="item.route"
                        as="InertiaLink"
                    >
                        {{ item.title }}
                    </Button>
                </nav>
            </aside>

            <section class="flex-1 md:max-w-2xl">
                <slot />
            </section>
        </div>
    </div>
</template>
