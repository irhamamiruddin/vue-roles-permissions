<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Users List
                <inertia-link :href="route('users.create')">
                    <JetButton class="float-right bg-green-500 hover:bg-green-600 active:bg-green-700">Create User</JetButton>
                </inertia-link>
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="flex flex-col">
                    <div class="overflow-x-auto sm:-mx-6 lg:-mx-8">
                        <div class="py-2 inline-block min-w-full sm:px-6 lg:px-8">
                            <div class="overflow-hidden">

                                <!-- Message -->
                                <!-- <div class="alert alert-success" v-if="$message = 'success'">
                                    <p>{{ $message }}</p>
                                </div> -->

                                <table class="min-w-full border text-center bg-white">
                                    <thead class="border-b bg-slate-400">
                                        <tr>
                                            <th scope="col" class="text-sm font-bold text-white px-6 py-4 border-r">
                                                No
                                            </th>
                                            <th scope="col" class="text-sm font-bold text-white px-6 py-4 border-r">
                                                Name
                                            </th>
                                            <th scope="col" class="text-sm font-bold text-white px-6 py-4 border-r">
                                                Email
                                            </th>
                                            <th scope="col" class="text-sm font-bold text-white px-6 py-4 border-r">
                                                Roles
                                            </th>
                                            <th scope="col" class="text-sm font-bold text-white px-6 py-4 border-r">
                                                Action
                                            </th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr v-if="!users.data.length">
                                            <td class="p-4 text-center text-gray-900" colspan="5">
                                                No data
                                            </td>
                                        </tr>
                                        <tr class="border-b" v-for="(user,i) in users.data" :key="user">
                                            <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900 border-r">
                                                {{ i+1 }}
                                            </td>
                                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border-r">
                                                {{ user.name }}
                                            </td>
                                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border-r">
                                                {{ user.email }}
                                            </td>
                                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border-r">
                                                <span v-for="role in user.roles" :key="role"
                                                    class="text-xs inline-block py-1 px-2.5 mx-1
                                                    leading-none text-center whitespace-nowrap align-baseline
                                                    font-bold bg-green-500 text-white rounded">
                                                    <label>{{ role.name }}</label>
                                                </span>
                                            </td>
                                            <td class="text-sm text-gray-900 font-light px-6 py-4 whitespace-nowrap border-r">
                                                <inertia-link
                                                    :href="route('users.show',user.id)"
                                                    class="font-bold text-sky-500 mx-1">
                                                    Show
                                                </inertia-link>
                                                <inertia-link
                                                    :href="route('users.edit',user.id)"
                                                    class="font-bold text-amber-500 mx-1">
                                                    Edit
                                                </inertia-link>
                                                <inertia-link
                                                    @click="deleteUser(user.id)"
                                                    class="font-bold text-red-500 mx-1">
                                                    Delete
                                                </inertia-link>
                                            </td>
                                        </tr>
                                    </tbody>
                                </table>
                                <JetPagination class="m-5" :links="users.links" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>

<script>
    import { InertiaLink } from '@inertiajs/inertia-vue3';
    import { Inertia } from '@inertiajs/inertia';
    import AppLayout from '@/Layouts/AppLayout.vue';
    import JetButton from '@/Jetstream/Button.vue';
    import JetPagination from '@/Components/Pagination.vue'

    export default{
        components:
        {
            AppLayout,
            JetButton,
            InertiaLink,
            JetPagination
        },

        props:['users','i'],

        methods:
        {
            deleteUser(data)
            {
                const result = confirm("Confirm delete user?");
                if (result) {
                    Inertia.delete(route("users.destroy", data));
                }
            },

        },

    };
</script>
