<template>
  <div class="flex-1 bg-[#0d0c0a] text-[#a8a095] p-10 overflow-y-auto space-y-8 flex flex-col items-center">
    <div class="text-center space-y-1 w-full max-w-2xl">
      <h1 class="text-4xl font-serif font-bold text-white">Tuner</h1>
      <p class="text-sm text-[#8c8275]">Chromatic guitar tuner</p>
    </div>

    <!-- Tuning Options -->
    <div class="flex flex-wrap items-center justify-center gap-2">
      <button class="px-4 py-1.5 rounded-xl bg-[#221d18] border border-[#e58e0d] text-white text-xs font-semibold">
        Standard
      </button>
      <button v-for="t in ['Drop D', 'Open G', 'Open E', 'DADGAD']" :key="t" class="px-4 py-1.5 rounded-xl bg-[#181512] border border-[#2a241e] hover:border-[#3b3228] text-xs text-[#a8a095] transition">
        {{ t }}
      </button>
    </div>

    <!-- Tuner Gauge Arc Display -->
    <div class="relative w-80 h-44 flex flex-col items-center justify-end">
      <!-- Arc Visualization -->
      <div class="w-72 h-36 rounded-t-full border-t-8 border-l-8 border-r-8 border-[#3b3228] relative overflow-hidden flex items-center justify-center">
        <div class="absolute inset-0 bg-gradient-to-r from-red-900/30 via-emerald-800/40 to-red-900/30"></div>
      </div>
      
      <!-- Needle Indicator -->
      <div class="absolute bottom-0 w-1 h-28 bg-[#e58e0d] rounded-full transform -rotate-12 origin-bottom shadow-lg"></div>
      <div class="w-4 h-4 rounded-full bg-[#e58e0d] z-10 -mt-2"></div>
    </div>

    <!-- Action Button -->
    <button class="bg-[#e58e0d] hover:bg-[#d4820b] text-slate-950 font-bold px-8 py-3 rounded-2xl text-sm transition shadow-lg shadow-[#e58e0d]/10">
      Start Tuner
    </button>

    <!-- Guitar String Frequencies Grid -->
    <div class="w-full max-w-2xl space-y-3 pt-4">
      <p class="text-[10px] font-bold uppercase tracking-widest text-[#5c544a] text-center">STANDARD (EADGBE)</p>
      <div class="grid grid-cols-6 gap-2">
        <div v-for="s in strings" :key="s.note" class="bg-[#181512] border border-[#2a241e] rounded-xl p-3 text-center space-y-1">
          <p class="text-xl font-bold text-white font-serif">{{ s.note }}</p>
          <p class="text-[10px] text-[#8c8275]">{{ s.freq }}</p>
          <p class="text-[9px] text-[#5c544a]">{{ s.string }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const strings = [
  { note: 'E', freq: '82.41 Hz', string: '6 (E2)' },
  { note: 'A', freq: '110 Hz', string: '5 (A2)' },
  { note: 'D', freq: '146.83 Hz', string: '4 (D3)' },
  { note: 'G', freq: '196 Hz', string: '3 (G3)' },
  { note: 'B', freq: '246.94 Hz', string: '2 (B3)' },
  { note: 'E', freq: '329.63 Hz', string: '1 (E4)' }
]
</script>