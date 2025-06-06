<script lang="ts">
  import '../../app.css';
  import { fade } from 'svelte/transition';
  import { slide } from 'svelte/transition';

  let isMobileMenuOpen = false;

  function toggleMobileMenu() {
    isMobileMenuOpen = !isMobileMenuOpen;
  }
</script>

<div class="min-h-screen flex flex-col bg-gradient-to-br from-surface to-gray-100 relative overflow-x-hidden">
  <!-- Background shapes -->
  <div class="fixed inset-0 pointer-events-none">
    <div class="absolute w-[300px] md:w-[400px] h-[300px] md:h-[400px] -top-24 -right-24 rounded-full bg-gradient-to-br from-primary to-primary-light opacity-10 blur-3xl animate-float"></div>
    <div class="absolute w-[200px] md:w-[300px] h-[200px] md:h-[300px] -bottom-12 -left-12 rounded-full bg-gradient-to-br from-primary to-primary-light opacity-10 blur-3xl animate-float-delay"></div>
    <div class="absolute w-[150px] md:w-[200px] h-[150px] md:h-[200px] top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 rounded-full bg-gradient-to-br from-primary to-primary-light opacity-10 blur-3xl animate-pulse"></div>
  </div>

  <!-- Navigation -->
  <nav class="sticky top-0 z-50 w-full bg-white/80 backdrop-blur-sm border-b border-gray-200/50 shadow-sm" transition:fade>
    <div class="container mx-auto px-4">
      <div class="flex items-center justify-between h-16">
        <!-- Logo/Home Link -->
        <div class="flex-shrink-0">
          <a href="/" class="flex items-center">
            <img src="/gordon-logo.png" alt="Gordon College Logo" class="h-8 w-auto" />
            <span class="ml-2 text-lg font-semibold text-primary hidden sm:block">Gordon College</span>
          </a>
        </div>

        <!-- Desktop Navigation -->
        <div class="hidden sm:flex sm:items-center sm:space-x-4">
          <a href="/" class="text-gray-700 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors">
            Home
          </a>
          <a href="/auth/login" class="text-gray-700 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors">
            Sign In
          </a>
          <a href="/auth/register" class="bg-primary text-white hover:bg-primary-light px-4 py-2 rounded-md text-sm font-medium transition-colors">
            Register
          </a>
        </div>

        <!-- Mobile menu button -->
        <div class="flex sm:hidden">
          <a href="/auth/login" class="mr-2 text-gray-700 hover:text-primary px-3 py-2 rounded-md text-sm font-medium transition-colors">
            Sign In
          </a>
          <a href="/auth/register" class="bg-primary text-white hover:bg-primary-light px-3 py-2 rounded-md text-sm font-medium transition-colors">
            Register
          </a>
        </div>
      </div>
    </div>
  </nav>

  <!-- Main content -->
  <main class="flex-1 flex flex-col items-center justify-center px-4 py-8" transition:fade>
    <div class="text-center mb-8 w-full max-w-md">
      <div class="inline-block p-4 bg-white rounded-full shadow-md mb-4 transition-transform hover:scale-105">
        <img src="/gordon-logo.png" alt="Gordon College Logo" class="w-12 h-12 sm:w-16 sm:h-16 object-contain" />
      </div>
      <h1 class="text-xl sm:text-2xl md:text-3xl font-bold text-primary mb-1">Gordon College</h1>
      <p class="text-sm sm:text-base text-gray-600">Olongapo City, Zambales</p>
    </div>

    <slot />
  </main>

  <!-- Footer -->
  <footer class="mt-auto w-full py-4 px-4 bg-white/80 backdrop-blur border-t border-gray-200" transition:fade>
    <div class="container mx-auto text-center">
      <p class="text-xs sm:text-sm text-gray-600">&copy; 2024 Gordon College. All rights reserved.</p>
    </div>
  </footer>
</div>

<style>
  /* Hide scrollbars but keep functionality */
  :global(body) {
    scrollbar-width: none; /* Firefox */
    -ms-overflow-style: none; /* IE and Edge */
  }
  
  :global(body::-webkit-scrollbar) {
    display: none; /* Chrome, Safari, Opera */
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-20px); }
  }

  @keyframes float-delay {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(20px); }
  }

  :global(.animate-float) {
    animation: float 8s ease-in-out infinite;
  }

  :global(.animate-float-delay) {
    animation: float-delay 12s ease-in-out infinite;
  }
</style> 