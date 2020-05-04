<template>
  <div>
    <b-table
      :data="data"
      :columns="columns">
      <b-input
          v-if="!props.column.numeric"
          slot="searchable"
          slot-scope="props"
          v-model="props.filters[props.column.field]"
          placeholder="Search..."
          icon="magnify"
          size="is-small" />
      
        <template slot-scope="props">
          <b-table-column field="orderId" width="40">
              {{ props.row.orderId }}
          </b-table-column>
          <b-table-column field="createdAt">
              <span class="tag is-success">
                {{ props.row.createdAt }}
              </span>
          </b-table-column>
          <b-table-column field="bank">
              {{ props.row.bank }}
          </b-table-column>
          <b-table-column field="amount" numeric>
              {{ new Intl.NumberFormat('id-ID', { maximumSignificantDigits: 3 }).format(props.row.amount) }}
          </b-table-column>
          <b-table-column field="note">
              {{ props.row.note }}
          </b-table-column>
          <b-table-column field="action">
              <b-button type="is-primary" @click="setPaid">Set Paid</b-button>
          </b-table-column>
        </template>
    </b-table>
  </div>
</template>

<script>
export default {
  name: 'Order',
  data() {
    return {
        data: [],
        columns: [
            {
                field: 'orderId',
                label: 'Order ID',
                searchable: true,
            },
            {
              field:'createdAt',
              label:'Payment At',
              searchable: true,
            },
            {
                field: 'bank',
                label: 'Bank',
                searchable: true,
            },
            {
                field: 'amount',
                label: 'Amount',
                searchable: true,
            },
            {
                field: 'note',
                label: 'Note',
                searchable: true,
            },
            {
              field: 'action',
              label: 'Action'
            }
        ]
    }
  },
  methods: {
    setPaid: function() {
      alert('test')
    }
  },
  mounted () {
    this.$http
      .get('https://love-ing.herokuapp.com/api/escrow')
      .then(response => (this.data = response.data))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
