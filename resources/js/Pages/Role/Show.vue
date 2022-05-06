<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Show Role
                <inertia-link :href="route('roles.index')">
                    <JetButton class="float-right bg-green-500 hover:bg-green-600 active:bg-green-700">Back</JetButton>
                </inertia-link>
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg p-3">
                    <p class="card-text mb-2 text-xl font-bold">Role {{ role.name }}</p>
                    <p class="card-text mb-2 text-lg font-semibold">Permissions :</p>
                    <div v-if="rolePermissions"> <!-- if rolePermissions empty -->
                        <p v-for="(permission,i) in rolePermissions" :key="permission">
                            {{ i+1 }}) {{ permission.name }}
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
    import { InertiaLink } from '@inertiajs/inertia-vue3';
    import AppLayout from '@/Layouts/AppLayout.vue';
    import JetButton from '@/Jetstream/Button.vue';

    export default{
        components:
        {
            AppLayout,
            InertiaLink,
            JetButton,
        },

        props:['role','rolePermissions'],

    };
</script>
