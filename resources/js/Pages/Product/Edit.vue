<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Create New Product
                <inertia-link :href="route('products.index')">
                    <JetButton class="float-right bg-green-500 hover:bg-green-600 active:bg-green-700">Back</JetButton>
                </inertia-link>
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <form>
                    <!-- Name -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="name" value="Name" />
                        <JetInput
                            id="name"
                            v-model="form.name"
                            type="text"
                            class="mt-1 block w-full"
                            autocomplete="name"
                        />
                        <JetInputError :message="$page.props.errors.name" class="mt-2" />
                    </div>

                    <!-- Detail -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="detail" value="Detail" />
                        <JetInput
                            id="detail"
                            v-model="form.detail"
                            type="text"
                            class="mt-1 block w-full"
                            autocomplete="detail"
                        />
                        <JetInputError :message="$page.props.errors.detail" class="mt-2" />
                    </div>

                    <JetButton
                        :type="'button'"
                        class="float-right bg-blue-500 hover:bg-blue-600 active:bg-blue-700"
                        @click="save(form)">
                        Save
                    </JetButton>

                </form>
            </div>
        </div>
    </AppLayout>
</template>

<script>
    import { InertiaLink } from '@inertiajs/inertia-vue3';
    import { Inertia } from '@inertiajs/inertia';
    import AppLayout from '@/Layouts/AppLayout.vue';
    import JetButton from '@/Jetstream/Button.vue';
    import JetFormSection from '@/Jetstream/FormSection.vue';
    import JetInput from '@/Jetstream/Input.vue';
    import JetInputError from '@/Jetstream/InputError.vue';
    import JetLabel from '@/Jetstream/Label.vue';
    import JetActionMessage from '@/Jetstream/ActionMessage.vue';

    export default{
        components:
        {
            AppLayout,
            JetButton,
            InertiaLink,
            JetActionMessage,
            JetFormSection,
            JetInput,
            JetInputError,
            JetLabel,
        },

        props:['product'],

        data(props) {
            return {
                form: {
                    id: this.product.id,
                    name: props.product.name,
                    detail: props.product.detail,
                },
            }
        },

        methods:
        {
            save(form) {
                Inertia.patch(route('products.update',this.product.id),form);
            },
        },

    };
</script>
