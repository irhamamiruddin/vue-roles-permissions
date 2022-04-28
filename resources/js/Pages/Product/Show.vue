<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Show Product
                <inertia-link :href="route('products.index')">
                    <JetButton class="float-right bg-green-500 hover:bg-green-600 active:bg-green-700">Back</JetButton>
                </inertia-link>
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg p-3">
                    <p class="card-text mb-2 text-lg font-semibold">Product Name : {{ product.name }}</p>
                    <p class="card-text mb-2 text-lg font-semibold">Details : {{ product.detail }}</p>
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

        props:['product'],

    };
</script>
