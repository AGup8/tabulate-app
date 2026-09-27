<template>
  <div class="flex-1 bg-[#0d0c0a] text-[#a8a095] flex overflow-hidden">
    <!-- Secondary Sub-Sidebar for Playlists & Songs -->
    <div class="w-60 border-r border-[#26221f] p-6 flex flex-col gap-6 shrink-0 bg-[#12100e]">
      <!-- Playlists Section -->
      <div class="space-y-3">
        <div class="flex items-center justify-between text-xs font-bold text-[#5c544a] tracking-wider uppercase">
          <span>Playlists</span>
          <button class="hover:text-white text-base">+</button>
        </div>
        <div class="space-y-1">
          <button class="w-full flex items-center justify-between px-3 py-2 rounded-xl bg-[#221d18] text-white text-sm font-medium border border-[#3b3228]">
            <span class="flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-[#e58e0d]"></span>
              <span>Beginner Songs</span>
            </span>
            <span class="text-xs text-[#736c63]">2</span>
          </button>
          <button class="w-full flex items-center justify-between px-3 py-2 rounded-xl hover:bg-[#1a1714] text-[#a8a095] text-sm font-medium transition">
            <span class="flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-emerald-500"></span>
              <span>Working On</span>
            </span>
            <span class="text-xs text-[#736c63]">2</span>
          </button>
          <button class="w-full flex items-center justify-between px-3 py-2 rounded-xl hover:bg-[#1a1714] text-[#a8a095] text-sm font-medium transition">
            <span class="flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-purple-400"></span>
              <span>Goals</span>
            </span>
            <span class="text-xs text-[#736c63]">1</span>
          </button>
        </div>
      </div>

      <!-- All Songs List -->
      <div class="space-y-3 flex-1 overflow-y-auto">
        <div class="text-xs font-bold text-[#5c544a] tracking-wider uppercase">
          All Songs
        </div>
        <div class="space-y-2 text-sm text-[#8c8275]">
          <p class="hover:text-white cursor-pointer transition">Wonderwall</p>
          <p class="hover:text-white cursor-pointer transition">House of the Rising Sun</p>
          <p class="hover:text-white cursor-pointer transition">Blackbird</p>
          <p class="hover:text-white cursor-pointer transition">Nothing Else Matters</p>
          <p class="hover:text-white cursor-pointer transition">Hotel California</p>
        </div>
      </div>
    </div>

    <!-- Main Content Area -->
    <div class="flex-1 p-10 overflow-y-auto space-y-6">
      <div>
        <h1 class="text-4xl font-serif font-bold text-white">Beginner Songs</h1>
        <p class="text-xs text-[#736c63] mt-1">2 songs</p>
      </div>

      <!-- Song Cards Grid -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <!-- Song Card 1 -->
        <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-6 space-y-4 hover:border-[#e58e0d]/40 transition cursor-pointer">
          <div class="flex items-start justify-between">
            <div>
              <h2 class="text-xl font-bold text-white">Wonderwall</h2>
              <p class="text-sm text-[#8c8275]">Oasis</p>
            </div>
            <span class="px-3 py-1 rounded-full bg-emerald-950/60 border border-emerald-800/40 text-emerald-400 text-xs font-medium">Beginner</span>
          </div>

          <!-- Chord Pills -->
          <div class="flex flex-wrap gap-1.5">
            <span v-for="c in ['Em7', 'G', 'Dsus4', 'A7sus4', 'Cadd9']" :key="c" class="px-2.5 py-1 bg-[#221d18] border border-[#332b23] rounded-lg text-xs font-mono text-[#d1c7bc]">
              {{ c }}
            </span>
          </div>

          <div class="flex items-center justify-between text-xs text-[#736c63] pt-2 border-t border-[#221d18]">
            <span>Key: D (capo 2)</span>
            <span>2026-09-10</span>
          </div>
        </div>

        <!-- Song Card 2 -->
        <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-6 space-y-4 hover:border-[#e58e0d]/40 transition cursor-pointer">
          <div class="flex items-start justify-between">
            <div>
              <h2 class="text-xl font-bold text-white">House of the Rising Sun</h2>
              <p class="text-sm text-[#8c8275]">The Animals</p>
            </div>
            <span class="px-3 py-1 rounded-full bg-emerald-950/60 border border-emerald-800/40 text-emerald-400 text-xs font-medium">Beginner</span>
          </div>

          <!-- Chord Pills -->
          <div class="flex flex-wrap gap-1.5">
            <span v-for="c in ['Am', 'C', 'D', 'F', 'E']" :key="c" class="px-2.5 py-1 bg-[#221d18] border border-[#332b23] rounded-lg text-xs font-mono text-[#d1c7bc]">
              {{ c }}
            </span>
          </div>

          <div class="flex items-center justify-between text-xs text-[#736c63] pt-2 border-t border-[#221d18]">
            <span>Key: Am</span>
            <span>2026-08-22</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>