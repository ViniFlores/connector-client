<template>
  <div class="flex flex-col items-center">
    <button class="fixed rounded transition duration-300 cursor-pointer bg-yellow-200 px-5 py-1 shadow-md hover:shadow-xl hover:bg-yellow-600 hover:text-white focus:outline-none" style="left: 16px; top: 16px;" @click="$router.push('/admin')">
      Admin
    </button>
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
      <card v-for="job in jobs" :key="job.id" class="mb-4" :logo="job.company_logo" v-bind="job" />
    </div>
  </div>
</template>

<script>
import { locations, descriptions } from '@/content/data'
import Autocomplete from '@/components/atoms/Autocomplete'
import Card from '@/components/molecules/Card'

export default {
  components: {
    Autocomplete,
    Card
  },
  title: 'Connector - Find your IT job and connect yourself',

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
          `https://clubedojournal.com.br/search?description=${this.selectedDescription}&location=${this.selectedLocation}`
        )
        .then((r) => {
          this.jobs = r
        })
    }
  }
}
</script>
