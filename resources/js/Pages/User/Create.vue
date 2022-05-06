<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Create New User
                <inertia-link :href="route('users.index')">
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

                    <!-- Email -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="email" value="Email" />
                        <JetInput
                            id="email"
                            v-model="form.email"
                            type="email"
                            class="mt-1 block w-full"
                            autocomplete="email"
                        />
                        <JetInputError :message="$page.props.errors.email" class="mt-2" />
                    </div>

                    <!-- Password -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="password" value="Password" />
                        <JetInput
                            id="password"
                            v-model="form.password"
                            type="password"
                            class="mt-1 block w-full"
                            required
                            autocomplete="new-password"
                        />
                        <JetInputError :message="$page.props.errors.password" class="mt-2" />
                    </div>

                    <!-- Confirm Password -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="confirm_password" value="Confirm Password" />
                        <JetInput
                            id="confirm_password"
                            v-model="form.confirm_password"
                            type="password"
                            class="mt-1 block w-full"
                            required
                            autocomplete="new-password"
                        />
                        <JetInputError :message="$page.props.errors.confirm_password" class="mt-2" />
                    </div>

                    <!-- Roles -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel class="font-bold" for="roles" value="Roles"/>
                            <select
                                class="form-multiselect block w-full mt-1 border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm"
                                id="roles" v-model="form.roles"
                                multiple>
                                <option
                                    v-for="role in roles" :key="role">
                                    {{ role }}
                                </option>
                            </select>
                        <JetInputError :message="$page.props.errors.roles" class="mt-2" />
                    </div>

                    <JetButton
                        :type="'button'"
                        class="float-right bg-blue-500 hover:bg-blue-600 active:bg-blue-700"
                        @click="createUser(form)">
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

        props:['roles'],

        data() {
            return {
                form: {
                    name: null,
                    email: null,
                    password: null,
                    confirm_password: null,
                    roles: [],
                },
            }
        },

        methods:
        {
            createUser(form){
                Inertia.post(route('users.store',form));
            }
        },

    };
</script>
