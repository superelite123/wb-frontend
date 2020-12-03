<template>
  <div class="main-content">
    <el-row class="header">
      <el-col :span="16">
        <img class=" wscnph" src="https://wpimg.wallstcn.com/b8a1d7be-0b73-41b8-be8c-7c01c93cab66.png" style="width:100px;height:100px">
      </el-col>
      <el-col :span="8">
        <p class="bolderP">{{ order.company_detail.companyname }}</p>
        <p class="lightP">{{ order.company_detail.address1 }}</p>
        <p class="lightP">
          {{ order.company_detail.city }}&nbsp;
          {{ order.company_detail.state }}&nbsp;
          {{ order.company_detail.zip }}&nbsp;
        </p>
        <p class="lightP">Cultivation LIC: CCL19-00006000</p>
        <p class="lightP">{{ order.company_detail.phone }}</p>
      </el-col>
    </el-row>
    <el-row>
      <el-col :span="8">
        <p class="bolderrP">INVOICE DATE:{{ order.date }}</p>
        <p class="bolderrP">INVOICE #:{{ order.number }}</p>
        <p class="bolderrP">METRC MANIFEST:{{ order.m_m_str }}</p>
        <p class="lightP">TERMS: {{ order.customer.termLabel }}</p>
        <p class="lightP">REP:{{ order.salesperson.firstname + ' ' + order.salesperson.lastname }}</p>
        <p class="lightP">REP PHONE:{{ order.customer.telephone }}</p>
      </el-col>
      <el-col :span="8">
        <p class="bolderP">{{ order.cname }}</p>
        <p class="lightP">{{ order.customer.address1 }}</p>
        <p class="lightP">
          {{ order.customer.city }}
          {{ order.customer.state_label }}
          {{ order.customer.zip }}
        </p>
        <p class="lightP">Phone: {{ order.customer.companyphone }}</p>
        <p class="lightP">Email:{{ order.customer.companyemail }}</p>
        <p class="lightP">License:{{ order.customer.licensenumber }}</p>
      </el-col>
      <el-col :span="8">
        <p class="bolderP">Distributor/Transporter</p>
        <p class="bolderP">{{ order.distuributor.companyname }}</p>
        <p class="lightP">
          {{ order.distuributor.address1 }},
          {{ order.distuributor.address2 }}
        </p>
        <p class="lightP">
          {{ order.distuributor.city }},
          {{ order.distuributor.state_label }}
          {{ order.distuributor.zipcode }}
        </p>
        <p class="lightP">
          Phone: {{ order.distuributor.phone }}
        </p>
        <p class="lightP">
          Email: {{ order.distuributor.email }}
        </p>
        <span class="lightP">License: </span><span class="bolderP">{{ order.distuributor.license }}</span>
      </el-col>
    </el-row>
    <template>
      <el-table
        :data="order.items"
        style="width: 100%"
      >
        <el-table-column
          prop="strain_label"
          label="Strain"
        />
        <el-table-column
          prop="p_type_label"
          label="Product Type"
        />
        <el-table-column
          prop="qty"
          label="Qty"
        />
        <el-table-column
          prop="units"
          label="Units"
        />
        <el-table-column
          prop="unit_price"
          label="Base Price"
        />
        <el-table-column
          prop="cpu"
          label="CPU"
        />
        <el-table-column
          prop="discount"
          label="Discount"
        />
        <el-table-column
          prop="dis_type"
          label="Discount Type"
        />
        <el-table-column
          prop="e_discount"
          label="Extra Discount"
        />
        <el-table-column
          prop="bp"
          label="Sub Total"
        />
        <el-table-column
          prop="extended"
          label="Extended"
        />
        <el-table-column
          prop="t_note"
          label="Line Note"
        />
        <el-table-column
          prop="ap"
          label="Adjust Total"
        />
      </el-table>
      <el-table
        :data="tableData"
        border
        style="width: 40%;margin-top:30px"
      >
        <el-table-column
          prop="date"
          label="Date"
          width="180"
        />
        <el-table-column
          prop="name"
          label="Name"
          width="180"
        />
        <el-table-column
          prop="address"
          label="Address"
        />
      </el-table>
    </template>
  </div>
</template>

<script>
import WBOrderResource from '@/api/wborder'
const wbOrderResource = new WBOrderResource()

export default {
  data() {
    return {
      article: '',
      fullscreenLoading: false,
      tableData: [{
        date: '2016-05-03',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      }, {
        date: '2016-05-02',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      }, {
        date: '2016-05-04',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      }, {
        date: '2016-05-01',
        name: 'Tom',
        address: 'No. 189, Grove St, Los Angeles'
      }],
      order: { company_detail: '', customer: '', salesperson: '' }
    }
  },
  mounted() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      this.order = await wbOrderResource.getOrderDetail(this.$route.query.id)
    }
  }
}
</script>

<style lang="scss">
@mixin clearfix {
  &:before {
    display: table;
    content: '';
    clear: both;
  }

  &:after {
    display: table;
    content: '';
    clear: both;
  }
}
@media print {
  table{
    font-size:1vw;
  }
}
.main-content{
  padding: 20px;
  margin: 0 auto;
  display: block;
  background: #fff;
}
.header{
  background:#e2e2e2;
  padding: 10px;
}
.bolderP{
  font-size:14px;
  font-weight: bolder;
}

.bolderrP{
  font-size:15px;
  font-weight: bolder;
}

.lightP{
  font-size:14px;
}
.content{
  margin: 20px 0 0;
  @include clearfix;
  font-size: 16px;
  color: #333;
  letter-spacing: 0.5px;
  line-height: 28px;
  margin-bottom: 30px;
}
</style>
