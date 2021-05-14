<template>
  <div class="flex flex-col items-center">
    <button class="fixed rounded transition duration-300 cursor-pointer bg-yellow-200 px-5 py-1 shadow-md hover:shadow-xl hover:bg-yellow-600 hover:text-white focus:outline-none" style="left: 16px; top: 16px;" @click="$router.push('/')">
      Application
    </button>
    <div class="py-5">
      <img src="logo.png" alt="">
    </div>
    <table class="table">
      <tr class="row header bg-yellow-600">
        <th v-for="header in headers" :key="header" class="cell">
          {{ header }}
        </th>
      </tr>
      <tr v-for="row in data" :key="row.id" class="row">
        <td v-for="header in headers" :key="`${row}-${header}`" class="cell text-center">
          {{ header != 'time' ? row[header] : $dayjs(row[header]).fromNow() }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data: () => ({
    headers: ['id', 'ip', 'location', 'description', 'time'],
    data: []
  }),

  head: () => ({
    title: 'Admin data - Connector'
  }),

  created () {
    this.fetchList()
  },

  methods: {
    fetchList () {
      this.$axios
        .$get(
          'https://clubedojournal.com.br/list'
        )
        .then((r) => {
          this.data = r.reverse()
        })
    }
  }
}
</script>

<style>
.table {
  width: 80%;
  display: table;
  margin: 0;
}

@media screen and (max-width: 768px) {
  .table {
    display: block;
  }
}

.row {
  display: table-row;
  background: #fff;
}

.row.header {
  color: #ffffff;
  background: #ED6337;
}

@media screen and (max-width: 768px) {
  .row {
    display: block;
  }

  .row.header {
    padding: 0;
    height: 0px;
  }

  .row.header .cell {
    display: none;
  }

  .row .cell:before {
    font-size: 12px;
    color: #808080;
    line-height: 1.2;
    text-transform: uppercase;
    font-weight: unset !important;

    margin-bottom: 13px;
    content: attr(data-title);
    min-width: 98px;
    display: block;
  }
}

.cell {
  display: table-cell;
}

@media screen and (max-width: 768px) {
  .cell {
    display: block;
  }
}

.row .cell {
  font-size: 15px;
  color: #666666;
  line-height: 1.2;
  font-weight: unset !important;

  padding-top: 20px;
  padding-bottom: 20px;
  border-bottom: 1px solid #f2f2f2;
}

.row.header .cell {
  font-size: 18px;
  color: #fff;
  line-height: 1.2;
  font-weight: unset !important;

  padding-top: 19px;
  padding-bottom: 19px;
}
</style>
