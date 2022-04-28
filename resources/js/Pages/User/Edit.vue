<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Edit User
                <inertia-link :href="route('users.index')">
                    <JetButton class="float-right bg-green-500 hover:bg-green-600 active:bg-green-700">Back</JetButton>
                </inertia-link>
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <form @submitted="createPost">
                    <!-- Name -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel for="name" value="Name" />
                        <JetInput
                            id="name"
                            v-model="form.name"
                            type="text"
                            class="mt-1 block w-full"
                            autocomplete="name"
                        />
                        <JetInputError :message="form.errors.name" class="mt-2" />
                    </div>

                    <!-- Email -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel for="email" value="Email" />
                        <JetInput
                            id="email"
                            v-model="form.email"
                            type="email"
                            class="mt-1 block w-full"
                            autocomplete="email"
                        />
                        <JetInputError :message="form.errors.email" class="mt-2" />
                    </div>

                    <!-- Password -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel for="password" value="Password" />
                        <JetInput
                            id="password"
                            v-model="form.password"
                            type="password"
                            class="mt-1 block w-full"
                            autocomplete="password"
                        />
                        <JetInputError :message="form.errors.password" class="mt-2" />
                    </div>

                    <!-- Confirm Password -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel for="confirm-password" value="Confirm Password" />
                        <JetInput
                            id="confirm-password"
                            type="password"
                            class="mt-1 block w-full"
                            autocomplete="confirm-password"
                        />
                        <JetInputError :message="form.errors.confirm-password" class="mt-2" />
                    </div>

                    <!-- Roles -->
                    <div class="col-span-6 sm:col-span-4 mb-4">
                        <JetLabel for="roles" value="Roles" />
                        <JetInput
                            id="roles"
                            type="text"
                            class="mt-1 block w-full"
                            autocomplete="roles"
                        />
                        <JetInputError :message="form.errors.roles" class="mt-2" />
                    </div>

                    <JetButton
                        class="float-right bg-blue-500 hover:bg-blue-600 active:bg-blue-700"
                        :class="{ 'opacity-25': form.processing }"
                        :disabled="form.processing">
                        Save
                    </JetButton>
                </form>
            </div>
        </div>
    </AppLayout>
</template>

<script>
    import { useForm } from '@inertiajs/inertia-vue3';
    import { InertiaLink } from '@inertiajs/inertia-vue3';
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

        props:['users','i','post'],

        methods:
        {
            deleteUser(postId)
            {
                const result = confirm("Confirm delete user?");
                if (result) {
                    Inertia.delete(route("users.destroy", postId), {
                        preserveScroll: true,
                    });
                }
            },
        },

        setup(props){
            const form = useForm({
                _method: 'POST',
                title: "",
                content: "",
            });
            const createPost = () => {
                form.post(route('users.store'));
            };
            return { form, createPost };
        }

    };
</script>
