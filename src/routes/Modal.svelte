<!-- Modal.svelte -->
<script>
    import { createEventDispatcher } from 'svelte';
  
    export let showModal;
    export let onClose;
  
    let name = '';
    let description = '';
    const dispatch = createEventDispatcher();
  
    function handleSave() {
        // Emit an event with the name value
        dispatch('save', { name, description });
        onClose(); // Close the modal
    }
  </script>
  
  <div class="{showModal ? 'fixed inset-0 flex items-center justify-center z-50' : 'hidden'}">
    <div class="fixed inset-0 bg-gray-900 opacity-50 z-40"></div>
  
    <div class="bg-white rounded-lg p-6 max-w-md w-full relative z-50">
      <div class="mb-4">
        <h2 class="text-lg font-bold mb-2">Define your shape</h2> <!-- Title -->
        <label for="name" class="block text-sm font-medium text-gray-700">Name:</label>
        <input type="text" id="name" bind:value={name} class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
      </div>
  
      <div class="mb-4">
        <label for="description" class="block text-sm font-medium text-gray-700">Description:</label>
        <textarea id="description" bind:value={description} class="mt-1 p-2 block w-full border-gray-300 rounded-md shadow-sm focus:ring-indigo-500 focus:border-indigo-500"></textarea>
      </div>
  
      <div class="flex justify-end">
        <button class="px-4 py-2 bg-blue-500 text-white rounded-md hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500" on:click={handleSave}>Save</button>
      </div>
    </div>
  </div>
  