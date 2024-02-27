<!-- page.svelte -->
<script>
    import Map from './Map.svelte';
</script>

<main class="p-4 flex flex-col items-center h-screen">
    <h1 class="text-2xl font-bold mb-4">Built for Zero Outreach Mapping</h1>
    
    <div class="w-full h-full overflow-hidden">
        <div class="w-full h-full">
            <Map />
        </div>
    </div>
</main>
