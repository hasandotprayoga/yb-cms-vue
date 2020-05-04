<template>
  <div>
      <b-table
        :columns="columns"
        :data="data"
        ref="table"
        detailed
        detail-key="id"
        @details-open="(row, index) => $buefy.toast.open(`Expanded ${row.id}`)"
        :show-detail-icon="showDetailIcon">
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
            <a @click="toggle(props.row)"> 
              {{ props.row.orderId }}
            </a>
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
          <b-table-column field="description">
              {{ props.row.description }}
          </b-table-column>
          <b-table-column field="action">
              <b-button type="is-primary" @click="setPaid(props.row.id)">Set Paid</b-button>
          </b-table-column>
        </template>

        <template slot="detail" slot-scope="props">
            <article class="media">
                <div class="media-content">
                    <div class="content">
                        <p>
                          <strong>{{ props.row.customerData.name }} | {{props.row.customerData.phone}}</strong>
                          <br>
                          <small>{{ props.row.customerData.email }}</small>
                            <small>31m</small>
                            <br>
                            Lorem ipsum dolor sit amet, consectetur adipiscing elit.
                            Proin ornare magna eros, eu pellentesque tortor vestibulum ut.
                            Maecenas non massa sem. Etiam finibus odio quis feugiat facilisis.
                        </p>
                    </div>
                </div>
            </article>
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
                field: 'description',
                label: 'Note',
                searchable: true,
            },
            {
              field: 'action',
              label: 'Action'
            }
        ],
        showDetailIcon: false
    }
  },
  methods: {
    setPaid: function(id) {
      alert(id)
    },
    toggle(row) {
      this.$refs.table.toggleDetails(row)
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
