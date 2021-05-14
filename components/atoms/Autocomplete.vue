<template>
  <div style="width: 180px;">
    <input
      v-model="input"
      style="width: 100%;"
      class="border-2 font-semibold border-gray-300 rounded-md px-2 transition duration-300 focus:outline-none focus:border-yellow-400 cursor-pointer bg-gray-100 hover:bg-white focus:bg-white"
      type="text"
      :placeholder="placeholder"
      @change="$emit('input', input)"
      @click="input = ''; $emit('input', input);"
      @focus="showDropdown = true"
      @blur="closeDropdown"
    >
    <div v-if="showDropdown" class="transition duration-300 ease-in-out absolute shadow-sm rounded-md border-2 border-gray-200 bg-gray-50 mt-2 overflow-hidden" style="width: 174px;">
      <div v-for="item in filteredItems" :key="item" class="py-2 transition duration-300 px-2 cursor-pointer border-l-4 border-gray-50 hover:border-yellow-600 hover:bg-yellow-400" @click="input = item; $emit('input', input)">
        {{ item }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    placeholder: {
      type: String,
      default: ''
    },
    items: {
      type: Array,
      default: () => []
    }
  },

  data: () => ({
    input: '',
    showDropdown: false
  }),

  computed: {
    filteredItems () {
      return this.items.filter(e => e.toLowerCase().includes(this.input.toLowerCase()))
    }
  },

  methods: {
    closeDropdown () {
      setTimeout(() => { this.showDropdown = false }, 200)
    }
  }
}
</script>
