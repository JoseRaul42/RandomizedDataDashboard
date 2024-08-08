<script lang="ts">
    import { onMount } from 'svelte';
    import { Chart, registerables } from 'chart.js';
    import type { ChartConfiguration } from 'chart.js';
    Chart.register(...registerables);
  
    let chartDiv: HTMLCanvasElement;
    let myChart: Chart<'bar', number[], string>;
  
    const data = {
      labels: [
        'January', 'February', 'March', 'April', 'May', 'June', 
        'July', 'August', 'September', 'October', 'November', 'December'
      ],
      datasets: [
        {
          label: 'Dataset 1',
          backgroundColor: 'rgba(255, 99, 132, 0.2)',
          borderColor: 'rgba(255, 99, 132, 1)',
          borderWidth: 1,
          data: [] as number[],
        },
      ],
    };
  
    const config: ChartConfiguration<'bar', number[], string> = {
      type: 'bar',
      data,
      options: {
        responsive: true,
        plugins: {
          legend: {
            position: 'top',
          },
          title: {
            display: true,
            text: 'Randomized Data Chart',
          },
        },
      },
    };
  
    function randomizeData() {
      data.datasets[0].data = Array.from({ length: 12 }, () => Math.floor(Math.random() * 100));
      myChart.update();
    }
  
    onMount(() => {
      myChart = new Chart(chartDiv, config);
      randomizeData();
    });
  
    export let triggerRandomize: () => void;
  
    triggerRandomize = randomizeData;
  </script>
  
  <div>
    <canvas bind:this={chartDiv}></canvas>
  </div>
  
  <style>
    div {
      width: 100%;
      height: 400px;
    }
  </style>
  