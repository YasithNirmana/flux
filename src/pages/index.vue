<template>
  <!-- <DashboardMenu /> -->
  <!-- <HelloWorld /> -->
  <v-container fluid>
    <v-row>
      <v-col cols="10">
        <h2 class="mb-3">Dashboard</h2>
      </v-col>
      <v-col cols="2" class="d-flex justify-end align-center">
        <!-- <v-btn size="small" variant="text">
          <span class="text-caption text-disabled">
            <v-icon icon="mdi-calendar" size="16" /> Time Period: 2023
          </span>
        </v-btn> -->
        <v-menu
          open-on-hover
        >
          <template v-slot:activator="{ props }">
            <v-btn
              size="small"
              variant="text"
              v-bind="props"
            >
              <span class="text-caption text-disabled">
                <v-icon icon="mdi-calendar" size="16" /> Time Period: {{ timePeriod.title }}
              </span>
            </v-btn>
          </template>

          <v-list>
            <v-list-item
              v-for="(item, index) in timePeriods"
              :key="index"
              :value="index"
              @click="selectedTimeIndex = index"
            >
              <v-list-item-title>{{ item.title }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="3">
        <v-card class="pa-2 d-flex flex-column justify-center" min-height="100" outlined>
          <div>
            <v-card-subtitle><v-icon icon="mdi-cash-multiple" /> Total Sales</v-card-subtitle>
            <v-row>
              <v-col class="pr-0 pb-0" cols="8">
                <v-card-title class="text-h5 pr-0">$300,000</v-card-title>
              </v-col>
              <v-col class="pl-0 pb-0" cols="4">
                <v-card-text class="pl-0 text-primary"><v-icon icon="mdi-arrow-top-right-thin" /> 2.5%</v-card-text>
              </v-col>
            </v-row>
          </div>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card class="pa-2 d-flex flex-column justify-center" min-height="100" outlined>
          <div>
            <v-card-subtitle><v-icon icon="mdi-cart" /> Total Orders</v-card-subtitle>
            <v-row>
              <v-col class="pr-0 pb-0" cols="8">
                <v-card-title class="text-h5 pr-0">1200</v-card-title>
              </v-col>
              <v-col class="pl-0 pb-0" cols="4">
                <v-card-text class="pl-0"><v-icon icon="mdi-arrow-bottom-right-thin" /> 2.5%</v-card-text>
              </v-col>
            </v-row>
          </div>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card class="pa-2 d-flex flex-column justify-center" min-height="100" outlined>
          <div>
            <v-card-subtitle><v-icon icon="mdi-cash" /> AOV</v-card-subtitle>
            <v-row>
              <v-col class="pr-0 pb-0" cols="8">
                <v-card-title class="text-h5 pr-0">$5000</v-card-title>
              </v-col>
              <v-col class="pl-0 pb-0" cols="4">
                <v-card-text class="pl-0"><v-icon icon="mdi-arrow-bottom-right-thin" /> 2.5%</v-card-text>
              </v-col>
            </v-row>
          </div>
        </v-card>
      </v-col>
      <v-col cols="3">
        <v-card class="pa-2 d-flex flex-column justify-center" min-height="100" outlined>
          <div>
            <v-card-subtitle><v-icon icon="mdi-cash" /> Active Orders</v-card-subtitle>
            <v-row>
              <v-col cols="6">
                <v-card-title class="text-h6 pr-0 pb-0">On Hold: 5</v-card-title>
              </v-col>
              <v-col cols="6">
                <v-card-title class="text-h6 pr-0 pb-0">In Process: 2</v-card-title>
              </v-col>
            </v-row>
          </div>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="6">
        <v-card class="pa-4" outlined>
          <v-card-title>Sales by Product Line</v-card-title>
          <Line
            id="sales-by-product-line-chart"
            :data="salesByProductLinechartData"
            :options="salesByProductLineChartOptions"
          />
        </v-card>
      </v-col>
      <v-col cols="6">
        <v-card class="pa-4" outlined>
          <v-card-title>Sales Overview</v-card-title>
          <Bar
            id="my-chart-id"
            :data="chartData"
            :options="chartOptions"
            :style="salesChartStyles"
          />
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="4">
        <v-card class="pa-4" outlined>
          <v-card-title>Top Performing Products</v-card-title>
          <div class="chart-container">
            <Pie 
              id="sales-by-category"
              :data="salesByProductPieChartData"
              :options="salesByProductPieChartOptions"
            />
          </div>
        </v-card>
      </v-col>
      <v-col cols="8">
        <v-card class="pa-4" outlined>
          <v-card-title>Recent Orders</v-card-title>
          <div style="max-height: 300px; overflow-y: auto; overscroll-behavior: contain;">
            <v-data-table
              :headers="[
                { title: 'Order ID', key: 'orderId' },
                { title: 'Customer', key: 'customer' },
                { title: 'Amount', key: 'amount' },
                { title: 'Status', key: 'status' },
              ]"
              :items="[
                { orderId: 101, customer: 'Alice', amount: '$250', status: 'Completed' },
                { orderId: 102, customer: 'Bob', amount: '$450', status: 'In Process' },
                { orderId: 103, customer: 'Charlie', amount: '$150', status: 'On Hold' },
                { orderId: 104, customer: 'David', amount: '$350', status: 'Completed' },
                { orderId: 105, customer: 'Alice', amount: '$250', status: 'Completed' },
                { orderId: 106, customer: 'Bob', amount: '$450', status: 'In Process' },
                { orderId: 107, customer: 'Charlie', amount: '$150', status: 'On Hold' },
                { orderId: 108, customer: 'David', amount: '$350', status: 'Completed' },
                { orderId: 109, customer: 'Charlie', amount: '$150', status: 'On Hold' },
                { orderId: 110, customer: 'David', amount: '$350', status: 'Completed' },
              ]"
              dense
              hide-default-footer
              fixed-header
            />
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts" setup>
  import {
    BarElement,
    CategoryScale,
    Chart as ChartJS,
    Legend,
    LinearScale,
    LineElement,
    PointElement,
    ArcElement,
    Title,
    Tooltip,
  } from 'chart.js'
  import { ref, computed } from 'vue'
  import { Bar, Line, Pie } from 'vue-chartjs'

  ChartJS.register(CategoryScale, LinearScale, BarElement, Title, Tooltip, Legend, LineElement, PointElement, ArcElement)

  const timePeriods = [
    { title: '2023' },
    { title: '2024' },
    { title: '2025' }
  ]

  // Selected time period index and computed current period
  const selectedTimeIndex = ref(0)
  const timePeriod = computed(() => timePeriods[selectedTimeIndex.value])

  const chartOptions: any = {
    responsive: true,
    maintainAspectRatio: true,
    plugins: {
      legend: { position: 'top' },
      title: { display: false },
    },
  }

  const chartData = ref({
    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
    datasets: [
      {
        label: 'Gross Margin ($)',
        backgroundColor: '#3b82f6',
        borderColor: '#2563eb',
        borderWidth: 1,
        data: [5, 5, 5, 5, 6, 9, 9, 12, 12, 15, 17, 14],
        barThickness: 15,
      },
      {
        label: 'Sales ($)',
        backgroundColor: '#EFA348',
        borderColor: '#EFA348',
        borderWidth: 1,
        data: [1, 2, 3, 4, 5, 6, 7, 8, 1, 2, 3, 4],
        barThickness: 15,
      },
    ],
  })

  const salesChartStyles = {
    width: '100%',
  }

  const salesByProductLineChartOptions: any = {
    responsive: true,
    maintainAspectRatio: true,
    plugins: {
      legend: { position: 'top' },
      title: { display: false },
    },
  }

  const salesByProductLinechartData = ref({
    labels: ['A', 'B', 'C', 'D', 'E', 'F', 'G'],
    datasets: [
      { 
        label: 'Data One', 
        backgroundColor: '#3b82f6',
        borderColor: '#3b82f6',
        data: [40, 39, 10, 40, 39, 80, 40],
      },
    ],
  })

  const salesByProductPieChartData = ref({
    labels: ['VueJs', 'EmberJs', 'ReactJs', 'AngularJs'],
    datasets: [
      {
        backgroundColor: ['#41B883', '#E46651', '#00D8FF', '#DD1B16'],
        data: [40, 20, 80, 10]
      }
    ]
  })

  const salesByProductPieChartOptions: any = {
    responsive: true,
    maintainAspectRatio: true
  }

</script>

<style scoped>
.chart-container {
  width: 300px;  /* Adjust this value to your needs */
  height: 300px; 
  margin: 0 auto; /* Centers the chart */
}
</style>
