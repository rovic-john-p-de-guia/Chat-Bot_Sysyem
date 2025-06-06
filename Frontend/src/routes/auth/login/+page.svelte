<script lang="ts">
  import { fade, fly } from 'svelte/transition';
  
  let email = '';
  let password = '';
  let showPassword = false;
  let isLoading = false;
  let error = '';

  function togglePassword() {
    showPassword = !showPassword;
  }

  async function handleSubmit() {
    error = '';
    if (!email || !password) {
      error = 'Please fill in all fields';
      return;
    }

    isLoading = true;
    try {
      // TODO: Implement actual login API call
      await new Promise(resolve => setTimeout(resolve, 1000));
      // Redirect to home page on success
      window.location.href = '/';
    } catch (err) {
      if (err instanceof Error) {
        error = err.message;
      } else {
        error = 'An error occurred';
      }
    } finally {
      isLoading = false;
    }
  }
</script>

<div class="w-full max-w-md mx-auto px-4 sm:px-0" transition:fly={{ y: 20, duration: 600 }}>
  <div class="bg-white/90 backdrop-blur p-6 sm:p-8 rounded-xl sm:rounded-2xl shadow-xl border border-white/50">
    <div class="text-center mb-6 sm:mb-8">
      <h2 class="text-2xl sm:text-3xl font-bold bg-gradient-to-r from-primary to-primary-light bg-clip-text text-transparent">
        Welcome Back
      </h2>
      <p class="text-sm sm:text-base text-gray-600 mt-1">Sign in to continue to GC Assistant</p>
    </div>

    <form on:submit|preventDefault={handleSubmit} class="space-y-5 sm:space-y-6">
      {#if error}
        <div class="flex items-center gap-2 p-3 sm:p-4 text-red-700 bg-red-50 rounded-lg border border-red-200 text-sm" transition:fade>
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 flex-shrink-0" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v3.75m9-.75a9 9 0 11-18 0 9 9 0 0118 0zm-9 3.75h.008v.008H12v-.008z" />
          </svg>
          <p>{error}</p>
        </div>
      {/if}

      <div class="space-y-1.5">
        <label for="email" class="text-sm font-medium text-gray-700">Email Address</label>
        <div class="relative">
          <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21.75 6.75v10.5a2.25 2.25 0 01-2.25 2.25h-15a2.25 2.25 0 01-2.25-2.25V6.75m19.5 0A2.25 2.25 0 0019.5 4.5h-15a2.25 2.25 0 00-2.25 2.25m19.5 0v.243a2.25 2.25 0 01-1.07 1.916l-7.5 4.615a2.25 2.25 0 01-2.36 0L3.32 8.91a2.25 2.25 0 01-1.07-1.916V6.75" />
            </svg>
          </div>
          <input
            type="email"
            id="email"
            bind:value={email}
            placeholder="example@gordoncollege.edu.ph"
            required
            class="w-full pl-10 pr-4 py-2 sm:py-2.5 text-sm sm:text-base rounded-lg border border-gray-300 focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
          />
        </div>
      </div>

      <div class="space-y-1.5">
        <label for="password" class="text-sm font-medium text-gray-700">Password</label>
        <div class="relative">
          <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16.5 10.5V6.75a4.5 4.5 0 10-9 0v3.75m-.75 11.25h10.5a2.25 2.25 0 002.25-2.25v-6.75a2.25 2.25 0 00-2.25-2.25H6.75a2.25 2.25 0 00-2.25 2.25v6.75a2.25 2.25 0 002.25 2.25z" />
            </svg>
          </div>
          <input
            type={showPassword ? 'text' : 'password'}
            id="password"
            bind:value={password}
            placeholder="Enter your password"
            required
            class="w-full pl-10 pr-12 py-2 sm:py-2.5 text-sm sm:text-base rounded-lg border border-gray-300 focus:ring-2 focus:ring-primary focus:border-transparent transition-all"
          />
          <button 
            type="button"
            class="absolute inset-y-0 right-0 pr-3 flex items-center text-gray-400 hover:text-primary transition-colors"
            on:click={togglePassword}
            aria-label={showPassword ? 'Hide password' : 'Show password'}
          >
            {#if showPassword}
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3.98 8.223A10.477 10.477 0 001.934 12C3.226 16.338 7.244 19.5 12 19.5c.993 0 1.953-.138 2.863-.395M6.228 6.228A10.45 10.45 0 0112 4.5c4.756 0 8.773 3.162 10.065 7.498a10.523 10.523 0 01-4.293 5.774M6.228 6.228L3 3m3.228 3.228l3.65 3.65m7.894 7.894L21 21m-3.228-3.228l-3.65-3.65m0 0a3 3 0 10-4.243-4.243m4.242 4.242L9.88 9.88" />
              </svg>
            {:else}
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.036 12.322a1.012 1.012 0 010-.639C3.423 7.51 7.36 4.5 12 4.5c4.638 0 8.573 3.007 9.963 7.178.07.207.07.431 0 .639C20.577 16.49 16.64 19.5 12 19.5c-4.638 0-8.573-3.007-9.963-7.178z" />
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
              </svg>
            {/if}
          </button>
        </div>
      </div>

      <div class="flex justify-end">
        <a href="/auth/forgot-password" class="text-sm font-medium text-primary hover:text-primary-light transition-colors">
          Forgot Password?
        </a>
      </div>

      <button
        type="submit"
        class="w-full flex items-center justify-center gap-2 py-2 sm:py-2.5 text-sm sm:text-base bg-gradient-to-r from-primary to-primary-light text-white rounded-lg font-medium shadow-md hover:shadow-lg transform hover:-translate-y-0.5 transition-all disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:transform-none"
        disabled={isLoading}
      >
        {#if isLoading}
          <svg class="animate-spin h-5 w-5" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
            <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
            <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
          </svg>
        {:else}
          Sign In
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 transition-transform group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13.5 4.5L21 12m0 0l-7.5 7.5M21 12H3" />
          </svg>
        {/if}
      </button>
    </form>

    <p class="mt-6 sm:mt-8 text-center text-sm text-gray-600">
      Don't have an account? 
      <a href="/auth/register" class="font-medium text-primary hover:text-primary-light transition-colors">
        Create an account
      </a>
    </p>
  </div>
</div>

<style>
  .auth-form-container {
    width: 100%;
    max-width: 440px;
    margin: 0 auto;
  }

  .auth-card {
    background: rgba(255, 255, 255, 0.9);
    padding: var(--spacing-xl);
    border-radius: var(--radius-lg);
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    backdrop-filter: blur(16px);
    border: 1px solid rgba(255, 255, 255, 0.5);
  }

  .card-header {
    text-align: center;
    margin-bottom: var(--spacing-xl);
  }

  h2 {
    color: var(--text);
    font-size: 2rem;
    font-weight: 700;
    margin-bottom: var(--spacing-xs);
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .subtitle {
    color: var(--text-light);
    margin-bottom: var(--spacing-xl);
  }

  .auth-form {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-lg);
  }

  .form-group {
    display: flex;
    flex-direction: column;
    gap: var(--spacing-xs);
  }

  label {
    color: var(--text);
    font-weight: 500;
    font-size: 0.875rem;
    display: flex;
    align-items: center;
    gap: var(--spacing-xs);
  }

  .input-container {
    position: relative;
    display: flex;
    align-items: center;
  }

  .input-icon {
    position: absolute;
    left: var(--spacing-md);
    width: 20px;
    height: 20px;
    color: var(--text-light);
  }

  .form-input {
    width: 100%;
    padding: var(--spacing-md);
    padding-left: calc(var(--spacing-md) * 2 + 20px);
    border: 1px solid var(--border);
    border-radius: var(--radius-md);
    font-size: 1rem;
    transition: all 0.2s;
    background: white;
  }

  .form-input:focus {
    outline: none;
    border-color: var(--primary);
    box-shadow: 0 0 0 4px rgba(0, 51, 102, 0.1);
  }

  .password-toggle {
    position: absolute;
    right: var(--spacing-md);
    color: var(--text-light);
    padding: 0.25rem;
    border-radius: var(--radius-sm);
    line-height: 0;
    transition: all 0.2s;
  }

  .password-toggle:hover {
    color: var(--primary);
    background: rgba(0, 51, 102, 0.1);
    transform: scale(1.1);
  }

  .password-toggle svg {
    width: 1.25rem;
    height: 1.25rem;
  }

  .form-options {
    display: flex;
    justify-content: flex-end;
    margin-top: calc(-1 * var(--spacing-md));
  }

  .forgot-link {
    color: var(--primary);
    text-decoration: none;
    font-size: 0.875rem;
    font-weight: 500;
    transition: all 0.2s;
  }

  .forgot-link:hover {
    color: var(--primary-light);
    transform: translateX(2px);
  }

  .submit-btn {
    background: linear-gradient(135deg, var(--primary) 0%, var(--primary-light) 100%);
    color: white;
    padding: var(--spacing-md);
    border-radius: var(--radius-md);
    font-weight: 500;
    font-size: 1rem;
    transition: all 0.2s;
    display: flex;
    justify-content: center;
    align-items: center;
    gap: var(--spacing-sm);
    height: 48px;
  }

  .submit-btn svg {
    width: 20px;
    height: 20px;
    transition: transform 0.2s;
  }

  .submit-btn:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 4px 6px -1px rgba(0, 51, 102, 0.2);
  }

  .submit-btn:hover:not(:disabled) svg {
    transform: translateX(4px);
  }

  .submit-btn:disabled {
    opacity: 0.7;
    cursor: not-allowed;
  }

  .loading-spinner {
    width: 20px;
    height: 20px;
    border: 2px solid white;
    border-top-color: transparent;
    border-radius: 50%;
    animation: spin 0.8s linear infinite;
  }

  @keyframes spin {
    to { transform: rotate(360deg); }
  }

  .error-message {
    background: #fee2e2;
    border: 1px solid #ef4444;
    color: #b91c1c;
    padding: var(--spacing-md);
    border-radius: var(--radius-md);
    font-size: 0.875rem;
    display: flex;
    align-items: center;
    gap: var(--spacing-sm);
  }

  .error-message svg {
    width: 20px;
    height: 20px;
    flex-shrink: 0;
  }

  .auth-footer-text {
    margin-top: var(--spacing-xl);
    text-align: center;
    font-size: 0.875rem;
    color: var(--text-light);
  }

  .auth-footer-text a {
    color: var(--primary);
    text-decoration: none;
    font-weight: 500;
    transition: all 0.2s;
  }

  .auth-footer-text a:hover {
    color: var(--primary-light);
    text-decoration: underline;
  }
</style> 