<script lang="ts">
	import { onMount } from 'svelte';
	import { page } from '$app/stores';
	import '../app.css';

	let isHeaderVisible = true;
	let lastScrollY = 0;

	onMount(() => {
		const handleScroll = () => {
			const currentScrollY = window.scrollY;
			isHeaderVisible = currentScrollY < lastScrollY || currentScrollY < 50;
			lastScrollY = currentScrollY;
		};

		window.addEventListener('scroll', handleScroll, { passive: true });

		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});
</script>

<div class="app-container">
	<header class="main-header" class:hidden={!isHeaderVisible}>
		<nav class="nav-container">
			<div class="logo">
				<a href="/">
					<img src="/gordon-logo.png" alt="Gordon College Logo" />
					<span>Gordon College</span>
				</a>
			</div>
			<div class="nav-links">
				{#if $page.url.pathname === '/'}
					<a href="#features">Features</a>
					<a href="#programs">Programs</a>
					<a href="#about">About</a>
					<a href="#contact">Contact</a>
				{/if}
				<a href="/auth/register" class="register-btn">Enroll Now</a>
			</div>
		</nav>
	</header>

	<main>
		<slot />
	</main>

</div>

<style>
	.app-container {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	header {
		background: var(--primary);
		color: white;
		border-bottom: 3px solid var(--secondary);
		position: sticky;
		top: 0;
		z-index: 10;
	}

	nav {
		max-width: 1200px;
		margin: 0 auto;
		padding: var(--spacing-md) var(--spacing-xl);
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.logo {
		display: flex;
		align-items: center;
		gap: var(--spacing-md);
	}

	.school-logo {
		height: 50px;
		width: auto;
	}

	.logo-text {
		display: flex;
		flex-direction: column;
	}

	.logo-text h1 {
		font-size: 1.5rem;
		font-weight: 600;
		color: white;
	}

	.subtitle {
		font-size: 0.875rem;
		color: var(--secondary);
	}

	ul {
		display: flex;
		gap: var(--spacing-xl);
		list-style: none;
	}

	li a {
		color: white;
		font-weight: 500;
		padding: var(--spacing-sm) var(--spacing-md);
		border-radius: var(--radius-md);
		transition: all 0.2s;
	}

	li a:hover, li a.active {
		background: rgba(255, 255, 255, 0.1);
		color: var(--secondary);
	}

	main {
		flex: 1;
		width: 100%;
		max-width: 1200px;
		margin: 0 auto;
		padding: var(--spacing-xl);
		padding-top: 72px; /* Height of the header */
	}

	footer {
		background: var(--primary);
		color: white;
		padding: var(--spacing-xl) 0;
		margin-top: auto;
	}

	.footer-content {
		max-width: 1200px;
		margin: 0 auto;
		padding: 0 var(--spacing-xl);
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: var(--spacing-xl);
	}

	.footer-section h3 {
		color: var(--secondary);
		margin-bottom: var(--spacing-md);
	}

	.footer-section ul {
		display: flex;
		flex-direction: column;
		gap: var(--spacing-sm);
	}

	.footer-section a:hover {
		color: var(--secondary);
	}

	.social-links {
		display: flex;
		gap: var(--spacing-md);
		margin-top: var(--spacing-sm);
	}

	.social-links a {
		background: rgba(255, 255, 255, 0.1);
		padding: var(--spacing-sm) var(--spacing-md);
		border-radius: var(--radius-sm);
		transition: all 0.2s;
	}

	.social-links a:hover {
		background: var(--secondary);
		color: var(--primary);
	}

	.footer-bottom {
		max-width: 1200px;
		margin: 0 auto;
		padding: var(--spacing-xl) var(--spacing-xl) 0;
		text-align: center;
		border-top: 1px solid rgba(255, 255, 255, 0.1);
		margin-top: var(--spacing-xl);
	}

	/* Header Styles */
	.main-header {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		background: white;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
		z-index: 1000;
		transition: transform 0.3s ease;
	}

	.main-header.hidden {
		transform: translateY(-100%);
	}

	.nav-container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 1rem var(--spacing-xl);
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	.logo a {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		text-decoration: none;
	}

	.logo img {
		height: 40px;
		width: auto;
	}

	.logo span {
		font-size: 1.25rem;
		font-weight: 600;
		color: var(--primary);
	}

	.nav-links {
		display: flex;
		gap: 2rem;
		align-items: center;
	}

	.nav-links a {
		color: var(--text);
		text-decoration: none;
		font-weight: 500;
		transition: color 0.2s;
	}

	.nav-links a:hover {
		color: var(--primary);
	}

	.login-btn {
		color: var(--primary) !important;
	}

	.register-btn {
		background: var(--primary);
		color: white !important;
		padding: 0.5rem 1rem;
		border-radius: var(--radius-md);
		transition: background-color 0.2s;
	}

	.register-btn:hover {
		background: var(--primary-light);
	}

	@media (max-width: 768px) {
		.nav-links {
			display: none;
		}
	}
</style>
