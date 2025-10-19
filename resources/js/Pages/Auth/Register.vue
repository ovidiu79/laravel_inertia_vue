<script setup>
    import { useForm } from '@inertiajs/vue3';
    import TextInput from '../Components/TextInput.vue';

    const form = useForm({
        name: null,
        email: null,
        password: null,
        password_confirmation: null,
        avatar: null,
        preview: null,
    })

    const change = (e) => {
        form.avatar = e.target.files[0]
        form.preview = URL.createObjectURL(e.target.files[0])
    }

    const submit = () => {
        form.post("/register", {
            preserveScroll: true,
            onError: () => form.reset("password", "password_confirmation"),
        });
    }
</script>

<template>
    <Head title="Register" />

    <h1 class="title">Register a new account</h1>

    <div class="w-2/4 mx-auto">
        <form>
            <div>
                <label for="avatar">Avatar</label>
                <input @input="change" type="file" id="avatar">
                <p class="error mt-2">{{ form.errors.avatar }}</p>
                <div class="m-auto mt-2">
                    <img class="object-cover w-28 h-28" :src="form.preview ? form.preview : 'storage/avatars/default.jpg'" alt="">
                </div>
            </div>

            <TextInput name="name" v-model="form.name" :message="form.errors.name" />
            <TextInput name="email" type="email" v-model="form.email" :message="form.errors.email" />
            <TextInput name="password" type="password" v-model="form.password" :message="form.errors.password" />
            <TextInput name="confirm password" type="password" v-model="form.password_confirmation" :message="form.errors.password_confirmation" />

            <div>
                <p class="text-slate-600 mb-2">Already a user? <a href="#" class="text-link">Login</a></p>
                <button @click.prevent="submit" class="primary-btn" :disabled="form.processing">Register</button>
            </div>
        </form>
    </div>
</template>
