<template>
  <div>
    <modal v-if="dialog">
      <div class="bg-white rounded-md px-8 py-8" style="max-width: 80vw;">
        <div class="flex items-center pb-2 border-b-2 border-gray-200">
          <img v-if="logo" style="max-width: 80px;" :src="logo" alt="">
          <img v-else style="max-width: 80px;" src="logo-placeholder.png" alt="">
          <div class="font-semibold mb-2 text-2xl mx-5">
            {{ company }}
          </div>
          <div class="ml-20">
            {{ title }}
          </div>
          <div v-if="type == 'Full Time'" class="bg-green-400 text-white px-2 rounded-md font-thin mx-2">
            Full Time
          </div>
          <div class="flex-grow" />
          <button class="font-black text-2xl px-5 focus:outline-none bg-yellow-100 hover:text-white transition duration-300 hover:bg-yellow-700 py-2" @click="dialog = false">
            X
          </button>
        </div>
        <div class="mt-5 border-b-2 border-gray-200 pb-2">
          <div class="overflow-scroll overflow-x-hidden bg-gray-100 rounded-md px-4 py-2 shadow" style="max-height: 600px;" v-html="description" />
        </div>
        <div class="mt-2 border-b-2">
          <span class="px-2 py-1 rounded-md text-white bg-green-500">
            How to apply:
          </span>
          <div class="overflow-scroll rounded-md px-4 mt-2 py-2 shadow" style="max-height: 200px;" v-html="how_to_apply" />
        </div>
      </div>
    </modal>
    <div class="flex border-2 border-gray-200 shadow-md mb-2 py-3 px-3 transition duration-300 bg-gray-100 cursor-pointer hover:bg-yellow-100 hover:shadow-2xl" @click="dialog = true">
      <div class="mr-2 flex flex-col px-2 overflow-ellipsis">
        <div class="font-semibold mb-2 text-lg">
          {{ company }}
        </div>
        <img v-if="logo" style="max-width: 80px;" :src="logo" alt="">
        <img v-else style="max-width: 80px;" src="logo-placeholder.png" alt="">
      </div>
      <div class="flex flex-col">
        <div class="flex flex-wrap">
          <div class="font-black mr-4">
            {{ title }}
          </div>
          <div class="text-yellow-600 font-semibold">
            {{ location }}
          </div>
          <div class="flex-grow" />
          <div v-if="type == 'Full Time'" class="bg-green-400 text-white px-2 rounded-md font-thin">
            Full Time
          </div>
          <div class="ml-3 text-semibold text-gray-500">
            {{ $dayjs(created_at).fromNow() }}
          </div>
        </div>
        <div class="overflow-ellipsis overflow-hidden leading-5 mt-2 text-gray-500 font-extralight break-words" v-html="description.substring(0,400) + ' ...'" />
      </div>
    </div>
  </div>
</template>

<script>
import Modal from '@/components/atoms/Modal'
export default {
  components: {
    Modal
  },
  props: {
    company: {
      type: String,
      default: null
    },
    logo: {
      type: String,
      default: null
    },
    title: {
      type: String,
      default: null
    },
    description: {
      type: String,
      default: null
    },
    location: {
      type: String,
      default: null
    },
    type: {
      type: String,
      default: null
    },
    created_at: {
      type: String,
      default: null
    },
    how_to_apply: {
      type: String,
      default: null
    }
  },
  data: () => ({
    dialog: false
  }),
  created () {
    console.log(this.how_to_apply)
  }
}
</script>
