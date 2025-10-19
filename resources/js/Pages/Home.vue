<script setup>
    defineProps({
        users: Object,
    })
</script>

<template>
    <Head :title="` | ${$page.component}`" />

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
         <div></div>
    </div>
</template>
