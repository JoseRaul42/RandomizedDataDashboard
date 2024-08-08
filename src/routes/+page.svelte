<script lang="ts">
    import Chart from '$lib/components/Chart.svelte';
    import { onMount } from 'svelte';
    import { Moon, Sun, Github } from 'lucide-svelte';
  
    let chartComponent: {
      triggerRandomize: () => void;
    };
  
    let isDarkMode = true;
  
    onMount(() => {
      if (isDarkMode) {
        document.documentElement.classList.add('dark');
      }
    });
  
    function toggleDarkMode() {
      isDarkMode = !isDarkMode;
      document.documentElement.classList.toggle('dark', isDarkMode);
    }
  
    function randomizeChartData() {
      if (chartComponent) {
        chartComponent.triggerRandomize();
      }
    }
  </script>
  
  <style>
    .header {
      background-color: hsl(var(--primary));
      color: hsl(var(--primary-foreground));
    }
    .sidebar {
      background-color: hsl(var(--card));
      color: hsl(var(--card-foreground));
    }
    .content {
      background-color: hsl(var(--background));
      color: hsl(var(--foreground));
    }
    .footer {
      background-color: hsl(var(--primary));
      color: hsl(var(--primary-foreground));
    }
    .nav-link {
      color: hsl(var(--foreground));
    }
    .nav-link:hover {
      background-color: hsl(var(--muted));
      color: hsl(var(--muted-foreground));
    }
    .dashboard-placeholder {
      border: 4px dashed hsl(var(--border));
      color: hsl(var(--foreground));
    }
  </style>
  
  <div class="min-h-screen flex flex-col">
    <header class="header p-4 flex justify-between items-center">
      <h1 class="text-2xl font-bold">Randomized Data Dashboard</h1>
      <button on:click={toggleDarkMode} class="p-2 rounded bg-lightblue-200 dark:bg-gray-800">
        <Sun class="h-6 w-6" />
      </button>
    </header>
    <div class="flex flex-1">
      <aside class="sidebar w-64 min-h-screen p-4">
        <nav>
          <ul>
            <li>
              <a href="https://github.com/JoseRaul42" class="nav-link block py-2 px-4" target="_blank">
                <Github class="inline-block h-6 w-6" />
                <span class="ml-2">GitHub</span>
              </a>
            </li>
          </ul>
        </nav>
      </aside>
      <main class="content flex-1 p-4">
        <div class="bg-white dark:bg-gray-900 p-6 shadow rounded-lg">
          <h2 class="text-xl font-semibold mb-4">Dashboard Overview</h2>
          <div class="dashboard-placeholder p-10 text-center">
            <Chart bind:this={chartComponent} />  </div>
        </div>
      </main>
    </div>
    <footer class="footer p-4 text-center">
      &copy; 2024 
      <a href="https://github.com/JoseRaul42" target="_blank" class="text-blue-500">
          <a href="https://github.com/JoseRaul42" class="nav-link block py-2 px-4" target="_blank">
                <Github class="inline-block h-6 w-6" />
                <span class="ml-2">GitHub</span>
              </a>
      </a>
    </footer>
  </div>
  