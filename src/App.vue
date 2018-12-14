<template>
  <div id="app" class="ui padded grid">
    <div class="ui row">
      <div class="twelve wide column">
        <expense-charts :chartData="datacollection"></expense-charts>
      </div>

      <div class="three wide column">
        <expense-list @updateChart='updateChart'></expense-list>
      </div>
    </div>
  </div>
</template>

<script>
import ExpenseList from './components/ExpenseList'
import ExpenseCharts from './components/ExpenseCharts'

export default {
  name: 'App',
  components: {
    ExpenseList,
    ExpenseCharts
  },
  data() {
    return {
      datacollection: {
        labels: ['2017-11-01'],
        datasets:[{
          label: 'Expenses',
          data: [13],
          backgroundColor: "#2bbbad",
          borderColor: "#2bbbad",
          fill: false
        }]

      }
    }
  },
    methods: {
    updateChart: function(expenselist) {
      let labels = [];
      let dataset = [];

      //sort expense list by date first
      expenselist.sort(function(a,b){
        return +new Date(a.date) - +new Date(b.date)
      })

      //save labels ( date )
      for (var i = 0; i < expenselist.length; i ++){
        if (i === 0){
          labels.push(expenselist[i].date)
          dataset.push(parseInt(expenselist[i].expense))
        }
        else{
          if (expenselist[i].date === expenselist[i-1].date){
            var amount = parseInt(expenselist[i].expense) + parseInt(dataset[dataset.length-1])
            dataset[dataset.length-1] = amount
          }
          else{
            labels.push(expenselist[i].date);
            dataset.push(parseInt(expenselist[i].expense))
          }
        }
      }
      this.datacollection = {
        labels: labels,
        datasets: [{
          label: 'Expenses',
          data: dataset,
          fill: false,
          backgroundColor: "#2bbbad",
          borderColor: "#2bbbad"
         }]
      }
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    color: #2c3e50;
    width: 100vw;
  }


</style>
