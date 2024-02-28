<!-- page.svelte -->
<script>
    import Map from './Map.svelte';
    import FeatureList from './FeatureList.svelte';
</script>

<main class="p-4 flex flex-col items-center h-screen bg-gray-200">    
    <div class="w-full h-full flex">
        <div class="container mx-auto px-4 sm:px-6 lg:px-8 w-1/4">
            <FeatureList />
        </div> 
        <div class="container mx-auto px-4 sm:px-6 lg:px-8">
            <Map />
        </div>
    </div>
</main>

