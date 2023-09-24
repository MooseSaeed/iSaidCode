<script setup>
import { Head, Link } from "@inertiajs/vue3";
import NavLayout from "@/Layouts/NavLayout.vue";

defineProps({
    canLogin: {
        type: Boolean,
    },
    canRegister: {
        type: Boolean,
    },
});
</script>

<template>
    <Head title="I Said Code" />

    <div class="relative min-h-screen bg-center bg-black bg-dark post-card">
        <NavLayout>
            <div v-if="canLogin" class="px-6 py-3 text-right">
                <Link
                    v-if="$page.props.auth.user"
                    :href="route('dashboard')"
                    class="font-semibold"
                    >Dashboard</Link
                >

                <template v-else>
                    <Link :href="route('login')" class="font-semibold"
                        >Log in</Link
                    >

                    <Link
                        v-if="canRegister"
                        :href="route('register')"
                        class="ml-4 font-semibold"
                        >Register</Link
                    >
                </template>
            </div>
        </NavLayout>
    </div>
</template>

<style></style>
