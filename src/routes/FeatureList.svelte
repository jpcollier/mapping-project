<script>
    import { shapesStore } from '../shapeStore.js';
  
    let features = [];
  
    // Subscribe to changes in shapesStore
    shapesStore.subscribe(value => {
      features = value;
    });
  
  </script>

<div class="divide-y divide-gray-200 overflow-hidden rounded-lg bg-white shadow">
    <div class="px-4 py-5 sm:px-6">
        <h1 class="text-l font-bold mb-4">Built for Zero Outreach Mapping Tool</h1>
        <p class="text-sm">This tool is designed to facilitate effective outreach efforts to support individuals experiencing homelessness in your community.</p>
        <br>
        <p class="text-sm">Once you draw and name an outreach area, it will populate below:</p>

    </div>
    <div class="px-4 py-5 sm:p-6">
        <ul>
            {#each features as feature (feature.name)}
              <li class="mb-4">
                <h2 class="text-l font-semibold">{feature.name}</h2>
                <p class="text-sm text-gray-700">{feature.description}</p>
              </li>
            {/each}
          </ul>
    </div>
  </div>
  
  
<!--   
  <div class="max-w-lg mx-auto">
    <h1 class="text-xl font-bold mb-4">Features</h1>
    <ul>
      {#each features as feature (feature.name)}
        <li class="mb-4">
          <h2 class="text-l font-semibold">{feature.name}</h2>
          <p class="text-gray-700">{feature.description}</p>
        </li>
      {/each}
    </ul>
  </div>
   -->