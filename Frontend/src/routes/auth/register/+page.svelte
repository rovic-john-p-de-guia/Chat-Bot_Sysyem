<script lang="ts">
  let formData = {
    firstName: '',
    lastName: '',
    email: '',
    studentId: '',
    password: '',
    confirmPassword: ''
  };
  
  let isLoading = false;
  let error = '';

  function validateForm() {
    if (!formData.firstName || !formData.lastName || !formData.email || 
        !formData.studentId || !formData.password || !formData.confirmPassword) {
      error = 'Please fill in all fields';
      return false;
    }

    if (formData.password !== formData.confirmPassword) {
      error = 'Passwords do not match';
      return false;
    }

    if (formData.password.length < 8) {
      error = 'Password must be at least 8 characters long';
      return false;
    }

    return true;
  }

  async function handleSubmit() {
    error = '';
    if (!validateForm()) return;

    isLoading = true;
    try {
      // TODO: Implement actual registration API call
      await new Promise(resolve => setTimeout(resolve, 1000));
      // Redirect to login page on success
      window.location.href = '/auth/login';
    } catch (err) {
      if (err instanceof Error) {
        error = err.message;
      } else {
        error = 'An error occurred during registration';
      }
    } finally {
      isLoading = false;
    }
  }
</script>

<div class="auth-form-container">
  <div class="auth-card">
    <h2>Create Account</h2>
    <p class="subtitle">Join Gordon College's online community</p>

    <form on:submit|preventDefault={handleSubmit} class="auth-form">
      {#if error}
        <div class="error-message">
          {error}
        </div>
      {/if}

      <div class="form-row">
        <div class="form-group">
          <label for="firstName">First Name</label>
          <input
            type="text"
            id="firstName"
            bind:value={formData.firstName}
            placeholder="Enter your first name"
            required
            class="form-input"
          />
        </div>

        <div class="form-group">
          <label for="lastName">Last Name</label>
          <input
            type="text"
            id="lastName"
            bind:value={formData.lastName}
            placeholder="Enter your last name"
            required
            class="form-input"
          />
        </div>
      </div>

      <div class="form-group">
        <label for="email">Email Address</label>
        <input
          type="email"
          id="email"
          bind:value={formData.email}
          placeholder="example@gordoncollege.edu.ph"
          required
          class="form-input"
        />
      </div>

      <div class="form-group">
        <label for="studentId">Student ID</label>
        <input
          type="text"
          id="studentId"
          bind:value={formData.studentId}
          placeholder="Enter your student ID"
          required
          class="form-input"
        />
      </div>

      <div class="form-group">
        <label for="password">Password</label>
        <input
          type="password"
          id="password"
          bind:value={formData.password}
          placeholder="Create a password"
          required
          class="form-input"
        />
        <span class="input-hint">Must be at least 8 characters long</span>
      </div>

      <div class="form-group">
        <label for="confirmPassword">Confirm Password</label>
        <input
          type="password"
          id="confirmPassword"
          bind:value={formData.confirmPassword}
          placeholder="Confirm your password"
          required
          class="form-input"
        />
      </div>

      <button type="submit" class="submit-btn" disabled={isLoading}>
        {#if isLoading}
          <span class="loading-spinner"></span>
        {:else}
          Create Account
        {/if}
      </button>
    </form>

    <p class="auth-footer-text">
      Already have an account? 
      <a href="/auth/login">Sign in</a>
    </p>
  </div>
</div>

<style>
  .auth-form-container {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
  }

  .auth-card {
    background: white;
    padding: var(--spacing-xl);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-lg);
  }

  h2 {
    color: var(--text);
    font-size: 1.75rem;
    font-weight: 600;
    margin-bottom: var(--spacing-xs);
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

  .form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: var(--spacing-md);
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
  }

  .form-input {
    width: 100%;
    padding: var(--spacing-md);
    border: 1px solid var(--border);
    border-radius: var(--radius-md);
    font-size: 1rem;
    transition: all 0.2s;
  }

  .form-input:focus {
    outline: none;
    border-color: var(--primary);
    box-shadow: 0 0 0 3px rgba(0, 51, 102, 0.1);
  }

  .input-hint {
    font-size: 0.75rem;
    color: var(--text-light);
  }

  .submit-btn {
    background: var(--primary);
    color: white;
    padding: var(--spacing-md);
    border-radius: var(--radius-md);
    font-weight: 500;
    font-size: 1rem;
    transition: all 0.2s;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 48px;
  }

  .submit-btn:hover:not(:disabled) {
    background: var(--primary-light);
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
  }

  .auth-footer-text a:hover {
    text-decoration: underline;
  }

  @media (max-width: 640px) {
    .form-row {
      grid-template-columns: 1fr;
    }
  }
</style> 