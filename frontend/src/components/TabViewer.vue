<template>
  <div class="flex-1 flex flex-col bg-slate-950 text-slate-100 overflow-hidden">
    <!-- Spotify-style Song Header Banner -->
    <div class="bg-gradient-to-b from-emerald-950/40 via-slate-900/60 to-slate-950 p-8 border-b border-slate-800/80 flex flex-col md:flex-row items-start md:items-end justify-between gap-6">
      <div class="space-y-2">
        <div class="flex items-center gap-2 text-xs font-semibold uppercase tracking-wider text-emerald-400">
          <span>Verified Tab</span>
          <span>•</span>
          <span>Standard Tuning (E A D G B E)</span>
        </div>
        <h1 class="text-4xl font-extrabold text-white tracking-tight">{{ song.title }}</h1>
        <p class="text-lg text-slate-400 font-medium">{{ song.artist }}</p>
      </div>

      <!-- Action Controls (Transpose, Capo, Autoscroll) -->
      <div class="flex flex-wrap items-center gap-3 bg-slate-900/90 border border-slate-800 p-2 rounded-xl backdrop-blur-md">
        <!-- Transpose Selector -->
        <div class="flex items-center gap-2 px-3 py-1.5 bg-slate-800/60 rounded-lg">
          <span class="text-xs font-semibold text-slate-400 uppercase">Key</span>
          <button @click="transpose(-1)" class="w-6 h-6 rounded bg-slate-700 hover:bg-emerald-500 hover:text-slate-950 font-bold text-xs flex items-center justify-center transition">-</button>
          <span class="text-sm font-bold text-emerald-400 min-w-[24px] text-center">{{ currentKey }}</span>
          <button @click="transpose(1)" class="w-6 h-6 rounded bg-slate-700 hover:bg-emerald-500 hover:text-slate-950 font-bold text-xs flex items-center justify-center transition">+</button>
        </div>

        <!-- Capo Indicator -->
        <div class="px-3 py-1.5 bg-slate-800/60 rounded-lg text-xs font-semibold text-slate-300">
          Capo: <span class="text-emerald-400">{{ song.capo === 0 ? 'None' : 'Fret ' + song.capo }}</span>
        </div>

        <!-- Auto-Scroll Toggle -->
        <button 
          @click="isScrolling = !isScrolling" 
          :class="isScrolling ? 'bg-emerald-500 text-slate-950' : 'bg-slate-800 text-slate-300 hover:bg-slate-700'"
          class="px-4 py-1.5 rounded-lg text-xs font-bold transition flex items-center gap-2">
          <span>{{ isScrolling ? '⏸ Pause Scroll' : '▶ Auto-Scroll' }}</span>
        </button>
      </div>
    </div>

    <!-- Song Tab Body Canvas (Monospaced & Synchronized Formatting) -->
    <div class="flex-1 overflow-y-auto p-8 space-y-8 font-mono">
      <div v-for="(section, idx) in song.sections" :key="idx" class="space-y-4 max-w-4xl">
        <!-- Section Header (e.g. [VERSE 1]) -->
        <div class="text-xs font-bold text-emerald-400 tracking-wider uppercase bg-emerald-950/30 border-l-2 border-emerald-500 px-3 py-1 inline-block rounded-r">
          {{ section.name }}
        </div>

        <!-- Lyrics & Chord Alignment Grid -->
        <div class="space-y-6 pl-2">
          <div v-for="(line, lineIdx) in section.lines" :key="lineIdx" class="leading-relaxed">
            <!-- Chord Row -->
            <div class="relative h-6 text-emerald-400 font-bold text-sm select-none">
              <span 
                v-for="(chord, cIdx) in line.chords" 
                :key="cIdx" 
                class="absolute hover:text-white hover:bg-emerald-600 px-1.5 py-0.5 rounded cursor-pointer transition shadow-sm"
                :style="{ left: chord.offset + 'ch' }">
                {{ chord.name }}
              </span>
            </div>
            <!-- Lyric Row -->
            <div class="text-slate-200 text-base font-sans tracking-wide">
              {{ line.lyric }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// Reactive state variables
const isScrolling = ref(false)
const currentKey = ref('Em')

// Mock Song Data structured according to our ChordJSON specification
const song = ref({
  title: 'Shape of My Heart',
  artist: 'Sting',
  capo: 2,
  sections: [
    {
      name: 'Verse 1',
      lines: [
        {
          lyric: 'He deals the cards as a meditation',
          chords: [
            { name: 'Em', offset: 0 },
            { name: 'D6', offset: 19 },
            { name: 'Am', offset: 32 },
            { name: 'B7sus4', offset: 45 },
            { name: 'B7', offset: 55 }
          ]
        },
        {
          lyric: 'And those he plays never suspect',
          chords: [
            { name: 'C/E', offset: 0 },
            { name: 'D6', offset: 19 },
            { name: 'Am', offset: 32 },
            { name: 'B7', offset: 45 }
          ]
        }
      ]
    },
    {
      name: 'Chorus',
      lines: [
        {
          lyric: 'I know that the spades are the swords of a soldier',
          chords: [
            { name: 'Cmaj7', offset: 0 },
            { name: 'G', offset: 22 },
            { name: 'D', offset: 36 }
          ]
        }
      ]
    }
  ]
})

function transpose(semitones) {
  // Simple keys array for demo transposition toggle
  const keys = ['C', 'C#', 'D', 'Eb', 'E', 'F', 'F#', 'G', 'Ab', 'A', 'Bb', 'B']
  console.log(`Transposing by ${semitones} semitone(s)`)
}
</script>