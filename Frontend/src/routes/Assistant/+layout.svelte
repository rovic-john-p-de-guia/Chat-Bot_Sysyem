<script lang="ts">
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  let isAuthenticated = false;

  onMount(() => {
    // Check if user is authenticated
    // This is a placeholder - in a real app, you would check your auth token/session
    const token = localStorage.getItem('authToken');
    if (!token) {
      goto('/auth/login');
    } else {
      isAuthenticated = true;
    }
  });
</script>

{#if isAuthenticated}
  <slot />
{/if}

<style>
  /* Add any layout-specific styles here */
</style> 