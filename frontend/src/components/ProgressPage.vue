<template>
  <div class="flex-1 bg-[#0d0c0a] text-[#a8a095] p-10 overflow-y-auto space-y-8">
    <div>
      <h1 class="text-4xl font-serif font-bold text-white">Progress</h1>
      <p class="text-sm text-[#8c8275] mt-1">Track your journey, song by song</p>
    </div>

    <!-- Stat Counter Cards -->
    <div class="grid grid-cols-2 md:grid-cols-4 gap-4">
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-5 space-y-1">
        <p class="text-3xl font-bold text-white font-serif">3</p>
        <p class="text-xs text-[#736c63]">Songs Learning</p>
      </div>
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-5 space-y-1">
        <p class="text-3xl font-bold text-white font-serif">7</p>
        <p class="text-xs text-[#736c63]">Recordings</p>
      </div>
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-5 space-y-1">
        <p class="text-3xl font-bold text-white font-serif">22m 06s</p>
        <p class="text-xs text-[#736c63]">Recorded Time</p>
      </div>
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-5 space-y-1">
        <p class="text-3xl font-bold text-white font-serif">6 🔥</p>
        <p class="text-xs text-[#736c63]">Day Streak</p>
      </div>
    </div>

    <!-- Timeline Divider -->
    <div class="relative flex items-center justify-center my-6">
      <div class="border-t border-[#26221f] w-full"></div>
      <span class="absolute bg-[#0d0c0a] px-4 text-[10px] font-bold uppercase tracking-widest text-[#5c544a]">
        SEPTEMBER 2026
      </span>
    </div>

    <!-- Recordings List -->
    <div class="space-y-3">
      <!-- Item 1 -->
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-4 flex items-center justify-between">
        <div class="flex items-center gap-4">
          <div class="w-10 h-10 rounded-xl bg-[#221d18] flex items-center justify-center text-[#e58e0d] text-base">
            🎵
          </div>
          <div>
            <h3 class="font-bold text-white text-base">Wonderwall</h3>
            <p class="text-xs text-[#736c63]">Oasis • 3 recordings • Last: Sep 24, 2026</p>
          </div>
        </div>
        <div class="flex items-center gap-2">
          <span class="px-3 py-1 rounded-full bg-[#221d18] text-[#e58e0d] text-xs font-semibold">Video</span>
          <span class="px-3 py-1 rounded-full bg-emerald-950/60 text-emerald-400 text-xs font-semibold">Audio</span>
        </div>
      </div>

      <!-- Item 2 -->
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-4 flex items-center justify-between">
        <div class="flex items-center gap-4">
          <div class="w-10 h-10 rounded-xl bg-[#221d18] flex items-center justify-center text-[#e58e0d] text-base">
            🎵
          </div>
          <div>
            <h3 class="font-bold text-white text-base">House of the Rising Sun</h3>
            <p class="text-xs text-[#736c63]">The Animals • 2 recordings • Last: Sep 17, 2026</p>
          </div>
        </div>
        <div class="flex items-center gap-2">
          <span class="px-3 py-1 rounded-full bg-[#221d18] text-[#e58e0d] text-xs font-semibold">Video</span>
          <span class="px-3 py-1 rounded-full bg-emerald-950/60 text-emerald-400 text-xs font-semibold">Audio</span>
        </div>
      </div>
    </div>
  </div>
</template>