<script setup>
    import { useForm } from '@inertiajs/vue3';
    import TextInput from '../Components/TextInput.vue';

    const form = useForm({
        name: null,
        email: null,
        password: null,
        password_confirmation: null,
        avatar: null,
    })

    const change = (e) => {
        form.avatar = e.target.files[0]
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
                <p>{{ form.errors.avatar }}</p>
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
