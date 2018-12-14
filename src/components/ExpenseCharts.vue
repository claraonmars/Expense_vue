<!-- <template>
  <div>
      <p>Chart goes here...</p>
  </div>
</template> -->

<script>
import { Line, mixins } from 'vue-chartjs'

export default {
  name: 'component-one',
  extends: Line,
  mixins: [mixins.reactiveProp],
  data(){
    return{
      options:{
        scales: {
        yAxes: [{
          ticks: {
            beginAtZero: true,
            min: 0
          }
        }]
      },
        responsive: true,
        maintainAspectRatio: false,
      }
    }
  },
  mounted () {
  this.renderChart(this.chartData, this.options)
  }
}
</script>

<style scoped>
div {
  color: white;
  background-color: white;
}
</style>
