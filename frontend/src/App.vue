<template>
  <div class="flex h-screen bg-[#0d0c0a] font-sans overflow-hidden select-none">
    <!-- Main Left Navigation Sidebar -->
    <Sidebar :activeTab="activeTab" @navigate="current => activeTab = current" />

    <!-- Active View Area -->
    <SearchPage v-if="activeTab === 'search'" />
    <LibraryPage v-else-if="activeTab === 'library'" />
    <ProgressPage v-else-if="activeTab === 'progress'" />
    <TunerPage v-else-if="activeTab === 'tuner'" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Sidebar from './components/Sidebar.vue'
import SearchPage from './components/SearchPage.vue'
import LibraryPage from './components/LibraryPage.vue'
import ProgressPage from './components/ProgressPage.vue'
import TunerPage from './components/TunerPage.vue'

const activeTab = ref('search')
</script>