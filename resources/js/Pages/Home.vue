<script setup>
import { ref, watch } from 'vue';
import {router} from '@inertiajs/vue3';
import { debounce } from 'lodash';

    const props = defineProps({
        users: Object,
        searchTerms: String
    })

    const search = ref(props.searchTerms);

    watch(
        search,
        debounce((q) => router.get('/', {search: q}, {preserveState: true}), 500),
    );
</script>

<template>
    <Head :title="` | ${$page.component}`" />

    <div>
        <div class="flex justify-end mb-4">
            <div class="w-1/4">
                <input type="search" placeholder="Search" v-model="search" />
            </div>
        </div>
    </div>

    <div>
        <table>
            <thead>
                <tr class="bg-slate-300">
                    <th>Avatar</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Registration Date</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="user in users.data" :key="user.id">
                    <td>
                        <img :src="user.avatar ? 'storage/' + user.avatar : 'storage/avatars/default.jpg'" class="avatar">
                    </td>
                    <td>{{ user.name }}</td>
                    <td>{{ user.email }}</td>
                    <td>{{ user.created_at }}</td>
                </tr>
            </tbody>
        </table>

        <!-- Pagination links -->
         <div>
            <Link v-for="link in users.links" :key="link.label" v-html="link.label" href="link.url" class="p-1 mx-1" :class="{'text-slate-300' : !link.url, 'text-blue-500' : link.active}"></Link>
         </div>
    </div>
</template>
