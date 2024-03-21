<template>
    <aside :class="`${is_expanded ? 'is-expanded' : ''}`" @mouseenter="ExpandMenu" @mouseleave="CollapseMenu">
        <div class="logo">
            <img :src="logoURL" alt="Vue" />
        </div>
        <div class="menu-toggle-wrap">
            <button class="menu-toggle bg-white border-0" @click="ToggleMenu">
                <span class="material-icons">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><path d="M0 96C0 78.3 14.3 64 32 64H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 128 0 113.7 0 96zM0 256c0-17.7 14.3-32 32-32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32c-17.7 0-32-14.3-32-32zM448 416c0 17.7-14.3 32-32 32H32c-17.7 0-32-14.3-32-32s14.3-32 32-32H416c17.7 0 32 14.3 32 32z"/></svg>
                </span>
            </button>
        </div>
        <div class="menu d-block">
            <router-link v-for="(item, index) in menuItems" :key="index" :to="item.route" class="button icon" :class="{ 'router-link-exact-active': item.route === '/' }">
                <span v-if="item.route === '/home' || item.route === '/about'" v-html="item.svgPath"></span>
                <span class="text">{{ item.label }}</span>
            </router-link>
        </div>
    </aside>
</template>

<script setup>
import { ref } from 'vue'
import logoURL from '@/assets/logo.svg';

const is_expanded = ref(localStorage.getItem("is_expanded") === "true")
const ToggleMenu = () => {
    is_expanded.value = !is_expanded.value
    localStorage.setItem("is_expanded", is_expanded.value)
}
const menuItems = [
    { label: 'Home', route: '/home', svgPath: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 576 512"><path d="M575.8 255.5c0 18-15 32.1-32 32.1h-32l.7 160.2c0 2.7-.2 5.4-.5 8.1V472c0 22.1-17.9 40-40 40H456c-1.1 0-2.2 0-3.3-.1c-1.4 .1-2.8 .1-4.2 .1H416 392c-22.1 0-40-17.9-40-40V448 384c0-17.7-14.3-32-32-32H256c-17.7 0-32 14.3-32 32v64 24c0 22.1-17.9 40-40 40H160 128.1c-1.5 0-3-.1-4.5-.2c-1.2 .1-2.4 .2-3.6 .2H104c-22.1 0-40-17.9-40-40V360c0-.9 0-1.9 .1-2.8V287.6H32c-18 0-32-14-32-32.1c0-9 3-17 10-24L266.4 8c7-7 15-8 22-8s15 2 21 7L564.8 231.5c8 7 12 15 11 24z"/></svg>' },
    { label: 'About', route: '/about', svgPath: '<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path d="M164.9 24.6c-7.7-18.6-28-28.5-47.4-23.2l-88 24C12.1 30.2 0 46 0 64C0 311.4 200.6 512 448 512c18 0 33.8-12.1 38.6-29.5l24-88c5.3-19.4-4.6-39.7-23.2-47.4l-96-40c-16.3-6.8-35.2-2.1-46.3 11.6L304.7 368C234.3 334.7 177.3 277.7 144 207.3L193.3 167c13.7-11.2 18.4-30 11.6-46.3l-40-96z"/></svg>' },
];
const ExpandMenu = () => {
    is_expanded.value = true;
}
const CollapseMenu = () => {
    is_expanded.value = false;
}
</script>