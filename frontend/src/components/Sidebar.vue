<template>
  <aside class="w-64 bg-[#141210] text-[#a8a095] flex flex-col justify-between border-r border-[#26221f] h-screen select-none shrink-0">
    <div>
      <!-- Brand Header -->
      <div class="p-6 flex items-center gap-3">
        <div class="w-10 h-10 rounded-xl bg-[#e58e0d] flex items-center justify-center text-slate-950 font-black text-xl shadow-md">
          🎸
        </div>
        <div>
          <h1 class="text-lg font-serif font-bold text-white tracking-wide">Tabulate</h1>
          <p class="text-xs text-[#736c63]">Guitar Learning Hub</p>
        </div>
      </div>

      <!-- Navigation Links -->
      <nav class="px-3 space-y-1.5 mt-2">
        <button 
          @click="$emit('navigate', 'search')"
          :class="[
            'w-full flex items-start gap-3.5 px-4 py-3 rounded-xl transition text-left group',
            activeTab === 'search' 
              ? 'bg-[#241f19] text-[#e58e0d] border border-[#e58e0d]/40 shadow-inner' 
              : 'hover:bg-[#1c1916] text-[#a8a095] hover:text-slate-200'
          ]">
          <span class="text-lg">🔍</span>
          <div>
            <div class="font-medium text-sm leading-none" :class="activeTab === 'search' ? 'text-white' : ''">AI Tab Finder</div>
            <div class="text-[11px] text-[#736c63] mt-1">Search & synthesize</div>
          </div>
        </button>

        <button 
          @click="$emit('navigate', 'library')"
          :class="[
            'w-full flex items-start gap-3.5 px-4 py-3 rounded-xl transition text-left group',
            activeTab === 'library' 
              ? 'bg-[#241f19] text-[#e58e0d] border border-[#e58e0d]/40 shadow-inner' 
              : 'hover:bg-[#1c1916] text-[#a8a095] hover:text-slate-200'
          ]">
          <span class="text-lg">📚</span>
          <div>
            <div class="font-medium text-sm leading-none" :class="activeTab === 'library' ? 'text-white' : ''">My Library</div>
            <div class="text-[11px] text-[#736c63] mt-1">Playlists & saved tabs</div>
          </div>
        </button>

        <button 
          @click="$emit('navigate', 'progress')"
          :class="[
            'w-full flex items-start gap-3.5 px-4 py-3 rounded-xl transition text-left group',
            activeTab === 'progress' 
              ? 'bg-[#241f19] text-[#e58e0d] border border-[#e58e0d]/40 shadow-inner' 
              : 'hover:bg-[#1c1916] text-[#a8a095] hover:text-slate-200'
          ]">
          <span class="text-lg">📈</span>
          <div>
            <div class="font-medium text-sm leading-none" :class="activeTab === 'progress' ? 'text-white' : ''">Progress</div>
            <div class="text-[11px] text-[#736c63] mt-1">Recordings & tracking</div>
          </div>
        </button>

        <button 
          @click="$emit('navigate', 'tuner')"
          :class="[
            'w-full flex items-start gap-3.5 px-4 py-3 rounded-xl transition text-left group',
            activeTab === 'tuner' 
              ? 'bg-[#241f19] text-[#e58e0d] border border-[#e58e0d]/40 shadow-inner' 
              : 'hover:bg-[#1c1916] text-[#a8a095] hover:text-slate-200'
          ]">
          <span class="text-lg">⏱️</span>
          <div>
            <div class="font-medium text-sm leading-none" :class="activeTab === 'tuner' ? 'text-white' : ''">Tuner</div>
            <div class="text-[11px] text-[#736c63] mt-1">Chromatic guitar tuner</div>
          </div>
        </button>
      </nav>
    </div>

    <!-- Bottom Profile Footer -->
    <div class="p-4 border-t border-[#26221f] flex items-center gap-3">
      <div class="w-8 h-8 rounded-full bg-[#241f19] border border-[#3b3228] flex items-center justify-center text-xs">
        🎸
      </div>
      <div>
        <p class="text-xs font-semibold text-slate-200">My Guitar Journey</p>
        <p class="text-[10px] text-[#736c63]">Tabulate v0.1 • Beta</p>
      </div>
    </div>
  </aside>
</template>

<script setup>
defineProps({
  activeTab: String
})

defineEmits(['navigate'])
</script>