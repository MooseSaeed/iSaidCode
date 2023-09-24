<script setup>
import { ref, onMounted, onUnmounted } from "vue";

defineProps({});

// Navbar animation
const lastScrollTop = ref(0);
const scrollingDown = ref(false);
const scrollingUp = ref(false);

onMounted(() => {
    window.addEventListener("scroll", handleScroll);
});
onUnmounted(() => {
    window.removeEventListener("scroll", handleScroll);
});
function handleScroll(e) {
    let st = window.pageYOffset || document.documentElement.scrollTop;
    if (st > lastScrollTop.value) {
        scrollingDown.value = true;
        scrollingUp.value = false;
    } else {
        scrollingDown.value = false;
        scrollingUp.value = true;
    }
    lastScrollTop.value = st <= 0 ? 0 : st; // For Mobile or negative scrolling
}
</script>

<template>
    <nav
        class="bg-white py-4 fixed w-full z-50 top-0 transition-all duration-700"
        :class="{
            '-translate-y-24 delay-300': scrollingDown,
        }"
    >
        <slot />
    </nav>
</template>
