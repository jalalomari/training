<template>
    <div class="header align-items-stretch px-10 bg-white">
        <div class="d-flex align-items-stretch justify-content-between flex-md-grow-1">
            <div>
                <div class="header-menu align-items-stretch">
                    <span class="py-4">
                        <span>
                            <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 261.76 226.69">
                                <path d="M161.096.001l-30.225 52.351L100.647.001H-.005l130.877 226.688L261.749.001z"
                                    fill="#41b883" />
                                <path d="M161.096.001l-30.225 52.351L100.647.001H52.346l78.526 136.01L209.398.001z"
                                    fill="#34495e" />
                            </svg>
                            Logo
                        </span>
                    </span>
                </div>
            </div>
            <div class="d-flex align-items-center d-none d-md-flex w-50 search-container">
                <div class="d-flex align-items-center d-none d-md-flex w-100 ">
                    <div class="col position-relative ">
                        <div class="input-group ">
                            <input v-model="searchQuery" class="form-control rounded form-control-solid border-primary"
                                 placeholder="Search..." />
                        </div>
                    </div>
                </div>
            </div>
            <div class="mt-3">
                <div>
                    <select class="form-select form-select-solid border-primary" v-model="selectedLanguage">
                        <option value="en">English</option>
                        <option value="ar">Arabic</option>
                    </select>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
const searchQuery = ref(''); 
const selectedLanguage = ref('en'); 
</script>

<style scoped>

</style>