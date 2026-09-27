<template>
  <div class="flex-1 bg-[#0d0c0a] text-[#a8a095] flex flex-col items-center justify-start p-8 overflow-y-auto">
    <!-- Search Hero Header -->
    <div class="w-full max-w-2xl text-center space-y-3 my-6">
      <h1 class="text-5xl font-serif italic font-bold text-white tracking-tight">Find the perfect tab</h1>
      <p class="text-sm text-[#8c8275] max-w-lg mx-auto leading-relaxed">
        Search for any song or artist. Select a track to explore AI-synthesized tabs and web sources.
      </p>
    </div>

    <!-- Live Search Box -->
    <div class="w-full max-w-2xl space-y-6">
      <div class="bg-[#181512] border border-[#2a241e] rounded-2xl p-4 shadow-2xl focus-within:border-[#e58e0d]/50 transition">
        <div class="flex items-center gap-3 px-2">
          <span class="text-lg text-[#696055]">🔍</span>
          <input 
            v-model="searchQuery"
            @focus="onSearchFocus"
            type="text" 
            placeholder="Search song title or artist (e.g., 'Wonderwall', 'Metallica')..." 
            class="w-full bg-transparent text-base text-white placeholder-[#696055] focus:outline-none"
          />
          <button 
            v-if="searchQuery" 
            @click="clearSearch"
            class="text-xs text-[#736c63] hover:text-white px-2 py-1 bg-[#221d18] rounded-lg transition">
            Clear
          </button>
        </div>
      </div>

      <!-- Stage 1: Dynamic Song Catalog Matches -->
      <div v-if="songResults.length > 0 && !selectedSong" class="space-y-3">
        <div class="flex items-center justify-between px-1">
          <span class="text-xs font-bold uppercase tracking-wider text-[#5c544a]">
            Songs Found ({{ songResults.length }})
          </span>
          <span class="text-xs text-[#736c63]">Select a song to view tab versions</span>
        </div>

        <div class="space-y-2">
          <div 
            v-for="song in songResults" 
            :key="song.id"
            @click="selectSong(song)"
            class="bg-[#181512] border border-[#2a241e] hover:border-[#e58e0d]/50 rounded-2xl p-4 flex items-center justify-between cursor-pointer transition group shadow-lg">
            
            <div class="flex items-center gap-4">
              <div class="w-12 h-12 rounded-xl bg-[#221d18] border border-[#332b23] flex items-center justify-center text-xl font-bold text-[#e58e0d]">
                🎵
              </div>
              <div>
                <h3 class="text-lg font-bold text-white group-hover:text-[#e58e0d] transition">{{ song.title }}</h3>
                <p class="text-sm text-[#8c8275]">{{ song.artist }} • <span class="text-[#a8a095]">{{ song.album }}</span> ({{ song.year }})</p>
              </div>
            </div>

            <div class="flex items-center gap-2 text-xs text-[#8c8275] group-hover:text-white transition">
              <span>{{ song.webSources.length + 1 }} Tab Sources</span>
              <span>→</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Stage 2: Tab Version Hub for Selected Song -->
      <div v-if="selectedSong" class="space-y-6 pt-2">
        <!-- Selected Track Summary Header -->
        <div class="bg-[#181512] border border-[#3b3228] rounded-2xl p-6 flex items-center justify-between">
          <div>
            <div class="flex items-center gap-2">
              <button 
                @click="selectedSong = null" 
                class="text-xs text-[#8c8275] hover:text-[#e58e0d] transition">
                ← All Songs
              </button>
              <span class="text-[#3b3228]">•</span>
              <span class="text-[10px] uppercase font-bold tracking-widest text-[#e58e0d]">Selected Track</span>
            </div>
            <h2 class="text-3xl font-serif font-bold text-white mt-1">{{ selectedSong.title }}</h2>
            <p class="text-sm text-[#8c8275] mt-0.5">
              {{ selectedSong.artist }} • <span class="text-[#a8a095]">{{ selectedSong.album }}</span> ({{ selectedSong.year }})
            </p>
          </div>
        </div>

        <!-- Flagship AI Tab Option -->
        <div class="space-y-2">
          <span class="text-xs font-bold uppercase tracking-wider text-[#e58e0d]">Flagship AI Synthesizer</span>
          <div 
            @click="loadTab(selectedSong.aiTab)"
            class="bg-gradient-to-r from-[#241a0e] via-[#1a1612] to-[#181512] border-2 border-[#e58e0d] rounded-2xl p-6 cursor-pointer hover:shadow-xl hover:shadow-[#e58e0d]/10 transition group">
            <div class="flex items-start justify-between">
              <div class="space-y-2">
                <div class="flex items-center gap-2">
                  <span class="px-2.5 py-0.5 rounded-full bg-[#e58e0d] text-slate-950 font-black text-[10px] uppercase tracking-wider">
                    ✨ AI Synthesized
                  </span>
                  <span class="text-xs text-emerald-400 font-semibold">99.4% Verified Accuracy</span>
                </div>
                <h3 class="text-xl font-bold text-white group-hover:text-[#e58e0d] transition">Tabulate Master Tab</h3>
                <p class="text-xs text-[#a8a095] max-w-lg">
                  Combined intelligence from Ultimate Guitar, Songsterr & YouTube. Features auto-aligned chord sheets, full transpose, and verified chord variations.
                </p>
              </div>
              <button class="bg-[#e58e0d] text-slate-950 font-bold px-5 py-2.5 rounded-xl text-xs uppercase tracking-wider shadow-lg">
                Play AI Tab
              </button>
            </div>
          </div>
        </div>

        <!-- External & Web Sources Options -->
        <div class="space-y-4 pt-2">
          <div class="flex flex-col gap-3">
            <div class="flex items-center justify-between">
              <span class="text-xs font-bold uppercase tracking-wider text-[#5c544a]">
                Web & Community Sources ({{ filteredSources.length }})
              </span>
            </div>

            <!-- Dynamic Filter Options -->
            <div class="flex items-center gap-1.5 overflow-x-auto pb-1">
              <button 
                v-for="filter in availableFilters" 
                :key="filter.name"
                @click="setFilter(filter.name)"
                :class="[
                  'px-3 py-1.5 rounded-xl text-xs font-medium transition flex items-center gap-1.5 border',
                  selectedFilter === filter.name 
                    ? 'bg-[#e58e0d] text-slate-950 font-bold border-[#e58e0d]' 
                    : 'bg-[#181512] border-[#2a241e] text-[#8c8275] hover:text-white'
                ]">
                <span>{{ filter.name }}</span>
                <span 
                  :class="[
                    'text-[10px] px-1.5 py-0.2 rounded-full font-bold',
                    selectedFilter === filter.name ? 'bg-slate-950/20 text-slate-950' : 'bg-[#221d18] text-[#736c63]'
                  ]">
                  {{ filter.count }}
                </span>
              </button>
            </div>
          </div>

          <!-- Web Source List -->
          <div class="space-y-2">
            <div 
              v-for="source in paginatedSources" 
              :key="source.id"
              @click="loadTab(source)"
              class="bg-[#181512] border border-[#2a241e] hover:border-[#3b3228] rounded-xl p-4 flex items-center justify-between cursor-pointer transition">
              
              <div class="flex items-center gap-3">
                <span class="text-lg">{{ source.icon }}</span>
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <p class="font-bold text-white text-sm">{{ source.name }}</p>
                    <span class="text-[10px] px-2 py-0.5 rounded bg-[#221d18] text-[#8c8275] border border-[#332b23]">
                      {{ source.platform }}
                    </span>
                  </div>

                  <!-- Dynamic Metadata Line -->
                  <div class="flex flex-wrap items-center gap-2 text-xs">
                    <template v-if="source.metadata">
                      <span 
                        v-if="source.metadata.difficulty" 
                        class="text-[10px] font-semibold px-1.5 py-0.5 rounded bg-[#27211a] text-[#e58e0d] border border-[#3d3122]">
                        {{ source.metadata.difficulty }}
                      </span>

                      <span v-if="source.metadata.key" class="text-[#a8a095]">Key: <strong class="text-white">{{ source.metadata.key }}</strong></span>
                      <span v-if="source.metadata.capo" class="text-[#8c8275]">Capo: <strong class="text-[#c4bbb0]">{{ source.metadata.capo }}</strong></span>

                      <span v-if="source.metadata.rating" class="text-amber-400 font-semibold flex items-center gap-1">
                        ★ {{ source.metadata.rating }}
                        <span v-if="source.metadata.ratingsCount" class="text-[#736c63] font-normal">({{ source.metadata.ratingsCount }})</span>
                      </span>

                      <span v-if="source.metadata.type" class="px-2 py-0.5 rounded bg-[#221d18] text-[10px] text-[#8c8275] border border-[#2a241e]">
                        {{ source.metadata.type }}
                      </span>
                    </template>

                    <span v-else class="text-xs italic text-[#736c63]">
                      ✨ AI Summary: {{ source.aiSummary }}
                    </span>
                  </div>
                </div>
              </div>

              <div class="flex items-center gap-3 shrink-0">
                <span v-if="source.action === 'parse'" class="text-xs text-[#e58e0d]">Standardize & View →</span>
                <span v-else-if="source.action === 'embed'" class="text-xs text-purple-400">Watch / Embed →</span>
                <span v-else-if="source.action === 'redirect'" class="text-xs text-blue-400">Open External ↗</span>
              </div>
            </div>
          </div>

          <!-- Structured Pagination Bar -->
          <div v-if="totalPages > 1" class="flex items-center justify-between pt-4 border-t border-[#221d18] text-xs text-[#8c8275]">
            <div>
              Showing <span class="font-bold text-white">{{ startIndex + 1 }}</span> to <span class="font-bold text-white">{{ Math.min(endIndex, filteredSources.length) }}</span> of <span class="font-bold text-white">{{ filteredSources.length }}</span> tabs
            </div>

            <div class="flex items-center gap-1">
              <button 
                @click="currentPage--" 
                :disabled="currentPage === 1"
                class="px-3 py-1.5 rounded-lg bg-[#181512] border border-[#2a241e] hover:bg-[#221d18] hover:text-white disabled:opacity-30 disabled:cursor-not-allowed transition">
                ‹ Prev
              </button>

              <button 
                v-for="page in totalPages" 
                :key="page"
                @click="currentPage = page"
                :class="[
                  'px-3 py-1.5 rounded-lg border transition font-bold',
                  currentPage === page 
                    ? 'bg-[#e58e0d] text-slate-950 border-[#e58e0d]' 
                    : 'bg-[#181512] border-[#2a241e] text-[#8c8275] hover:text-white'
                ]">
                {{ page }}
              </button>

              <button 
                @click="currentPage++" 
                :disabled="currentPage === totalPages"
                class="px-3 py-1.5 rounded-lg bg-[#181512] border border-[#2a241e] hover:bg-[#221d18] hover:text-white disabled:opacity-30 disabled:cursor-not-allowed transition">
                Next ›
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const searchQuery = ref('')
const songResults = ref([])
const selectedSong = ref(null)

const selectedFilter = ref('All')
const currentPage = ref(1)
const itemsPerPage = 3

const mockSongCatalog = [
  {
    id: 's1',
    title: 'Wonderwall',
    artist: 'Oasis',
    album: "(What's the Story) Morning Glory?",
    year: '1995',
    aiTab: { id: 'ai-wonderwall', title: 'Wonderwall (Synthesized)' },
    webSources: [
      { id: 'w1', name: 'Official Chords Ver 1', platform: 'Ultimate Guitar', icon: '🎸', action: 'parse', metadata: { difficulty: 'Novice', key: 'F#m', capo: '2nd Fret', rating: '4.9', ratingsCount: '12,400', type: 'Chords + Lyrics' } },
      { id: 'w2', name: 'Songsterr Interactive Engine', platform: 'Songsterr', icon: '🎼', action: 'redirect', metadata: { difficulty: 'Intermediate', key: 'Em', capo: 'None', rating: '4.8', ratingsCount: '3,210', type: 'Interactive Audio' } },
      { id: 'w3', name: 'Marty Music Video Lesson', platform: 'YouTube', icon: '📺', action: 'embed', aiSummary: '18-min video breakdown covering the verse strumming pattern and capo position.' },
      { id: 'w4', name: 'Acoustic Fingerstyle Arrangement', platform: 'Ultimate Guitar', icon: '📄', action: 'parse', metadata: { difficulty: 'Intermediate', key: 'Em', capo: 'None', rating: '4.6', ratingsCount: '850', type: 'Fingerstyle Tab' } },
      { id: 'w5', name: 'Official Songbook PDF', platform: 'PDF', icon: '📕', action: 'redirect', aiSummary: 'Scanned sheet music with lead vocals and standard guitar tab lines.' },
      { id: 'w6', name: 'Interactive Chord Chart', platform: 'Chordify', icon: '🎹', action: 'redirect', metadata: { difficulty: 'Novice', key: 'F#m', capo: '2nd Fret', type: 'Auto-scrolling Chords' } },
      { id: 'w7', name: 'Easy Beginner Chords Ver 3', platform: 'Ultimate Guitar', icon: '🎸', action: 'parse', metadata: { difficulty: 'Absolute Beginner', key: 'G', capo: '2nd Fret', rating: '4.5', ratingsCount: '412', type: 'Simplified Chords' } },
      { id: 'w8', name: 'GuitarZeroToHero Video Tutorial', platform: 'YouTube', icon: '📺', action: 'embed', aiSummary: 'Detailed step-by-step tutorial with on-screen chords and rhythm diagram.' }
    ]
  },
  {
    id: 's2',
    title: 'House of the Rising Sun',
    artist: 'The Animals',
    album: 'The Animals',
    year: '1964',
    aiTab: { id: 'ai-house', title: 'House of the Rising Sun (Synthesized)' },
    webSources: [
      { id: 'w9', name: 'Chords Ver 1', platform: 'Ultimate Guitar', icon: '🎸', action: 'parse', metadata: { difficulty: 'Novice', key: 'Am', capo: 'None', rating: '4.8', ratingsCount: '8,100', type: 'Chords + Arpeggio' } },
      { id: 'w10', name: 'JustinGuitar Video Lesson', platform: 'YouTube', icon: '📺', action: 'embed', aiSummary: '6/8 time signature arpeggio picking pattern tutorial for beginners.' }
    ]
  }
]

const availableFilters = computed(() => {
  if (!selectedSong.value) return []
  const sources = selectedSong.value.webSources

  const counts = {}
  sources.forEach(s => {
    counts[s.platform] = (counts[s.platform] || 0) + 1
  })

  const filters = [{ name: 'All', count: sources.length }]
  Object.keys(counts).forEach(platform => {
    filters.push({ name: platform, count: counts[platform] })
  })

  return filters
})

const filteredSources = computed(() => {
  if (!selectedSong.value) return []
  if (selectedFilter.value === 'All') return selectedSong.value.webSources
  return selectedSong.value.webSources.filter(s => s.platform.toLowerCase() === selectedFilter.value.toLowerCase())
})

const totalPages = computed(() => Math.max(1, Math.ceil(filteredSources.value.length / itemsPerPage)))
const startIndex = computed(() => (currentPage.value - 1) * itemsPerPage)
const endIndex = computed(() => startIndex.value + itemsPerPage)

const paginatedSources = computed(() => {
  return filteredSources.value.slice(startIndex.value, endIndex.value)
})

watch(searchQuery, (newQuery) => {
  selectedSong.value = null
  selectedFilter.value = 'All'
  currentPage.value = 1
  if (!newQuery.trim()) {
    songResults.value = []
    return
  }
  const q = newQuery.toLowerCase()
  songResults.value = mockSongCatalog.filter(s => 
    s.title.toLowerCase().includes(q) || s.artist.toLowerCase().includes(q)
  )
})

function setFilter(filterName) {
  selectedFilter.value = filterName
  currentPage.value = 1
}

function onSearchFocus() {
  if (selectedSong.value) {
    selectedSong.value = null
  }
}

function clearSearch() {
  searchQuery.value = ''
  songResults.value = []
  selectedSong.value = null
  selectedFilter.value = 'All'
  currentPage.value = 1
}

function selectSong(song) {
  selectedFilter.value = 'All'
  currentPage.value = 1
  selectedSong.value = song
}

function loadTab(tabSource) {
  alert(`Loading tab view for: ${tabSource.name || tabSource.title}`)
}
</script>