<template>
  <div class="flex flex-col items-center">
    <div class="pt-5">
      <img src="logo.png" alt="">
    </div>
    <div class="flex pt-5 flex-wrap items-center justify-center">
      <autocomplete v-model="selectedDescription" class="pr-2 my-2" :items="descriptions" placeholder="Description" />
      <autocomplete v-model="selectedLocation" class="pr-2 my-2" :items="locations" placeholder="Location" />
      <button class="focus:outline-none transition duration-300 px-2 my-2 rounded-md bg-yellow-600 text-white hover:bg-yellow-500 focus:border-0" type="button" @click="fetchJobs">
        Find it !
      </button>
    </div>

    <div class="flex flex-col mt-5" style="max-width: 80vw;">
      <div v-for="job in jobs" :key="job.id" class="flex border-2 border-gray-200 shadow-md mb-2 py-3 px-3 bg-gray-100">
        <div class="mr-2 flex flex-col px-2 overflow-ellipsis">
          <div class="font-semibold mb-2 text-lg">
            {{ job.company }}
          </div>
          <img v-if="job.company_logo" style="max-width: 80px;" :src="job.company_logo" alt="">
          <img v-else style="max-width: 80px;" src="logo-placeholder.png" alt="">
        </div>
        <div class="flex flex-col">
          <div class="flex flex-wrap">
            <div class="font-black mr-4">
              {{ job.title }}
            </div>
            <div class="text-yellow-600 font-semibold">
              {{ job.location }}
            </div>
            <div class="flex-grow" />
            <div v-if="job.type == 'Full Time'" class="bg-green-400 text-white px-2 rounded-md font-thin">
              Full Time
            </div>
            <div class="ml-3 text-semibold text-gray-500">
              {{ $dayjs(job.created_at).fromNow() }}
            </div>
          </div>
          <div class="overflow-ellipsis overflow-hidden leading-5 mt-2 text-gray-500 font-extralight break-words" v-html="job.description.substring(0,400) + ' ...'" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { locations, descriptions } from '@/content/data'
import Autocomplete from '@/components/atoms/Autocomplete'

export default {
  components: {
    Autocomplete
  },

  data: () => ({
    selectedDescription: null,
    selectedLocation: null,
    jobs: [],

    locations,
    descriptions
  }),

  methods: {
    fetchJobs () {
      this.$axios
        .$get(
          `/api/positions.json?description=${this.selectedDescription}&location=${this.selectedLocation}`
        )
        .then((r) => {
          console.log(r)
          this.jobs = r
        })
    }
  }
}
</script>
