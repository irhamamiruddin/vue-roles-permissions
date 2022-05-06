<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Create New Roles
                <inertia-link :href="route('roles.index')">
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

                    <!-- Permissions -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="permission" value="Permissions" />
                        <div v-for="permission in permissions" :key="permission">
                            <JetCheckbox
                                v-model:checked="form.permissions"
                                :value="permission.name"
                                id="permission">
                            </JetCheckbox>
                            {{ permission.name }}
                        </div>
                        <JetInputError :message="$page.props.errors.permission" class="mt-2" />
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
    import {Inertia} from '@inertiajs/inertia';
    import AppLayout from '@/Layouts/AppLayout.vue';
    import JetButton from '@/Jetstream/Button.vue';
    import JetFormSection from '@/Jetstream/FormSection.vue';
    import JetInput from '@/Jetstream/Input.vue';
    import JetInputError from '@/Jetstream/InputError.vue';
    import JetLabel from '@/Jetstream/Label.vue';
    import JetActionMessage from '@/Jetstream/ActionMessage.vue';
    import JetCheckbox from '@/Jetstream/Checkbox.vue';

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
            JetCheckbox,
        },

        props:['permissions'],

        data() {
            return {
                form: {
                    name: null,
                    permissions: [],
                },
            }
        },

        methods:
        {
            save(data) {
                Inertia.post(route('roles.store', data));
            },
        }
    };
</script>
