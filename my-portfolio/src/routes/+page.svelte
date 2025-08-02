<!-- src/routes/+page.svelte -->
<script lang="ts">
	import { onMount } from 'svelte';

	// Portfolio data
	let name = 'Horace Njoroge';
	let title = 'Software Engineer';
	let status = 'building cool stuff';
	let email = 'your.email@example.com';
	let linkedin = 'https://linkedin.com/in/yourprofile';
	let github = 'https://github.com/yourusername';
	let bio = 'Passionate full-stack developer with 5+ years of experience building scalable web applications. I love creating elegant solutions to complex problems and working with cutting-edge technologies. When I\'m not coding, you can find me exploring new frameworks, contributing to open source, or mentoring upcoming developers.';

	// Dark mode state
	let isDark = false;
	let greeting = '';

	// Initialize dark mode and greeting on mount
	onMount(() => {
		const hour = new Date().getHours();
		
		// Set greeting based on time
		if (hour < 12) greeting = 'Good Morning';
		else if (hour < 17) greeting = 'Good Afternoon';
		else greeting = 'Good Evening';
		
		// Check for saved dark mode preference, otherwise use time-based default
		const savedMode = localStorage.getItem('darkMode');
		isDark = savedMode ? JSON.parse(savedMode) : (hour >= 18 || hour <= 6);
		
		updateTheme();
	});

	// Improved theme function
	function updateTheme() {
		if (typeof document !== 'undefined') {
			document.documentElement.classList.toggle('dark', isDark);
		}
	}

	// Toggle dark mode with persistence
	function toggleDarkMode() {
		isDark = !isDark;
		localStorage.setItem('darkMode', JSON.stringify(isDark));
		updateTheme();
	}

	const skills = [
		{ name: 'React', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg' },
		{ name: 'React Native', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/react/react-original.svg' },
		{ name: 'Svelte', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/svelte/svelte-original.svg' },
		{ name: 'Next.js', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nextjs/nextjs-original.svg' },
		{ name: 'TypeScript', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg' },
		{ name: 'Python', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg' },
		{ name: 'Node.js', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/nodejs/nodejs-original.svg' },
		{ name: 'NestJS', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nestjs/nestjs-original.svg' },
		{ name: 'PostgreSQL', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/postgresql/postgresql-original.svg' },
		{ name: 'MongoDB', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mongodb/mongodb-original.svg' },
		{ name: 'Docker', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg' },
		{ name: 'Kubernetes', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/kubernetes/kubernetes-plain.svg' },
		{ name: 'AWS', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/amazonwebservices/amazonwebservices-plain-wordmark.svg' },
		{ name: 'Prometheus', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/prometheus/prometheus-original.svg' },
		{ name: 'Grafana', icon: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/grafana/grafana-original.svg' }
	];

	const projects = [
		{
			id: 1,
			title: 'Event Ticketing Platform',
			description: 'Microservices platform with CI/CD and monitoring',
			tech: ['NestJS', 'Docker', 'PostgreSQL', 'K8s'],
			github: 'https://github.com/yourusername/event-ticketing',
			demo: '/projects/event-ticketing'
		},
		{
			id: 2,
			title: 'Real-time Chat App',
			description: 'Scalable chat with WebSocket and Redis',
			tech: ['Svelte', 'Node.js', 'Socket.io', 'Redis'],
			github: 'https://github.com/yourusername/chat-app',
			demo: '/projects/chat-app'
		},
		{
			id: 3,
			title: 'E-commerce API',
			description: 'RESTful API with payment processing',
			tech: ['TypeScript', 'Express', 'MongoDB'],
			github: 'https://github.com/yourusername/ecommerce-api',
			demo: '/projects/ecommerce-api'
		},
		{
			id: 4,
			title: 'Task Management',
			description: 'Productivity app with drag-and-drop',
			tech: ['React', 'Node.js', 'PostgreSQL'],
			github: 'https://github.com/yourusername/task-app',
			demo: '/projects/task-app'
		}
	];

	// Navigate to project detail
	function viewProject(projectId) {
		window.location.href = `/projects/${projectId}`;
	}
</script>

<svelte:head>
	<title>{name} - {title}</title>
	<meta name="description" content="{name} is a {title} passionate about building amazing web applications" />
	<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Crimson+Text:ital,wght@0,400;0,600;1,400&display=swap" rel="stylesheet">
</svelte:head>

<!-- Dark mode toggle -->
<button 
	on:click={toggleDarkMode}
	class="fixed top-4 right-4 z-50 p-2.5 rounded-lg bg-white dark:bg-gray-800 shadow-lg border border-gray-200 dark:border-gray-700 hover:shadow-xl transition-all duration-300"
	aria-label="Toggle dark mode"
>
	{#if isDark}
		<svg class="w-4 h-4 text-yellow-500" fill="currentColor" viewBox="0 0 20 20">
			<path fill-rule="evenodd" d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z" clip-rule="evenodd"></path>
		</svg>
	{:else}
		<svg class="w-4 h-4 text-gray-700" fill="currentColor" viewBox="0 0 20 20">
			<path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path>
		</svg>
	{/if}
</button>

<!-- Main Content -->
<div class="h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100 dark:from-gray-900 dark:via-gray-800 dark:to-gray-900 transition-all duration-500 overflow-hidden">
	<div class="h-full max-w-7xl mx-auto px-6 py-6 flex flex-col">
		
		<!-- Top Section: Hero + Projects -->
		<div class="grid grid-cols-1 lg:grid-cols-5 gap-8 mb-8 flex-shrink-0">
			
			<!-- Hero Section -->
			<div class="lg:col-span-2">
				<div class="flex flex-col lg:flex-row items-center lg:items-start gap-6 mb-8">
					<!-- Profile Image -->
					<div class="relative flex-shrink-0">
						<img 
							src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=140&h=140&fit=crop&crop=face" 
							alt="Profile" 
							class="w-28 h-28 rounded-full object-cover border-4 border-white dark:border-gray-700 shadow-xl"
						/>
						<div class="absolute -bottom-1 -right-1 w-6 h-6 bg-green-500 rounded-full border-3 border-white dark:border-gray-700 animate-pulse"></div>
					</div>
					
					<div class="flex-1 text-center lg:text-left">
						<!-- Name & Title -->
						<h1 class="text-3xl lg:text-4xl font-bold text-gray-900 dark:text-white mb-2">
							{name}
						</h1>
						<p class="text-xl text-gray-600 dark:text-gray-400 mb-2">
							{title}
						</p>
						<p class="text-sm text-green-600 dark:text-green-400 font-medium mb-6">
							{status}
						</p>
						
						<!-- Contact Links -->
						<div class="grid grid-cols-2 gap-3">
							<a 
								href="mailto:{email}" 
								class="inline-flex items-center justify-center px-4 py-2.5 bg-blue-600 hover:bg-blue-700 dark:bg-blue-700 dark:hover:bg-blue-800 text-white rounded-lg text-sm font-medium transition-colors duration-200 shadow-md"
							>
								<svg class="w-4 h-4 mr-2" fill="currentColor" viewBox="0 0 20 20">
									<path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z"></path>
									<path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z"></path>
								</svg>
								Email
							</a>
							<a 
								href={linkedin}
								target="_blank" 
								class="inline-flex items-center justify-center px-4 py-2.5 bg-blue-700 hover:bg-blue-800 dark:bg-blue-800 dark:hover:bg-blue-900 text-white rounded-lg text-sm font-medium transition-colors duration-200 shadow-md"
							>
								<svg class="w-4 h-4 mr-2" fill="currentColor" viewBox="0 0 20 20">
									<path fill-rule="evenodd" d="M16.338 16.338H13.67V12.16c0-.995-.017-2.277-1.387-2.277-1.39 0-1.601 1.086-1.601 2.207v4.248H8.014v-8.59h2.559v1.174h.037c.356-.675 1.227-1.387 2.526-1.387 2.703 0 3.203 1.778 3.203 4.092v4.711zM5.005 6.575a1.548 1.548 0 11-.003-3.096 1.548 1.548 0 01.003 3.096zm-1.337 9.763H6.34v-8.59H3.667v8.59zM17.668 1H2.328C1.595 1 1 1.581 1 2.298v15.403C1 18.418 1.595 19 2.328 19h15.34c.734 0 1.332-.582 1.332-1.299V2.298C19 1.581 18.402 1 17.668 1z" clip-rule="evenodd"></path>
								</svg>
								LinkedIn
							</a>
							<a 
								href={github}
								target="_blank" 
								class="inline-flex items-center justify-center px-4 py-2.5 bg-gray-900 dark:bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-600 text-white rounded-lg text-sm font-medium transition-colors duration-200 shadow-md"
							>
								<svg class="w-4 h-4 mr-2" fill="currentColor" viewBox="0 0 20 20">
									<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"></path>
								</svg>
								GitHub
							</a>
							<a 
								href="/resume.pdf" 
								target="_blank" 
								class="inline-flex items-center justify-center px-4 py-2.5 bg-purple-600 hover:bg-purple-700 text-white rounded-lg text-sm font-medium transition-colors duration-200 shadow-md"
							>
								<svg class="w-4 h-4 mr-2" fill="currentColor" viewBox="0 0 20 20">
									<path fill-rule="evenodd" d="M3 17a1 1 0 011-1h12a1 1 0 110 2H4a1 1 0 01-1-1zm3.293-7.707a1 1 0 011.414 0L9 10.586V3a1 1 0 112 0v7.586l1.293-1.293a1 1 0 111.414 1.414l-3 3a1 1 0 01-1.414 0l-3-3a1 1 0 010-1.414z" clip-rule="evenodd"></path>
								</svg>
								Resume
							</a>
						</div>
					</div>
				</div>
				
				<!-- Bio Section -->
				<div class="bg-white/70 dark:bg-gray-800/70 backdrop-blur-sm rounded-xl p-6 border border-gray-200/50 dark:border-gray-700/50 shadow-lg">
					<h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-4">About Me</h3>
					<p class="text-gray-700 dark:text-gray-300 leading-relaxed font-serif text-base">
						{bio}
					</p>
				</div>
			</div>
			
			<!-- Projects Section -->
			<div class="lg:col-span-3">
				<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-6 text-center lg:text-left">Featured Projects</h2>
				<div class="grid grid-cols-1 md:grid-cols-2 gap-4 h-full max-h-96">
					{#each projects as project}
						<div class="bg-white/70 dark:bg-gray-800/70 backdrop-blur-sm rounded-lg p-4 shadow-md border border-gray-200/50 dark:border-gray-700/50 hover:shadow-lg hover:-translate-y-0.5 transition-all duration-300 flex flex-col">
							<h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-2 line-clamp-1">
								{project.title}
							</h3>
							<p class="text-gray-600 dark:text-gray-400 text-sm leading-relaxed mb-3 flex-1 line-clamp-2">
								{project.description}
							</p>
							
							<!-- Tech Stack -->
							<div class="flex flex-wrap gap-1 mb-3">
								{#each project.tech as tech}
									<span class="bg-gray-100 dark:bg-gray-700 text-gray-700 dark:text-gray-300 px-2 py-0.5 rounded text-xs font-medium">
										{tech}
									</span>
								{/each}
							</div>
							
							<!-- Project Links -->
							<div class="flex gap-2 mt-auto">
								<a 
									href={project.github}
									target="_blank"
									class="flex-1 inline-flex items-center justify-center px-2 py-1.5 bg-gray-900 dark:bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-600 text-white rounded text-xs font-medium transition-colors duration-200"
								>
									<svg class="w-3 h-3 mr-1" fill="currentColor" viewBox="0 0 20 20">
										<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"></path>
									</svg>
									Code
								</a>
								<button 
									on:click={() => viewProject(project.id)}
									class="flex-1 inline-flex items-center justify-center px-2 py-1.5 bg-blue-600 hover:bg-blue-700 text-white rounded text-xs font-medium transition-colors duration-200"
								>
									<svg class="w-3 h-3 mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z"></path>
									</svg>
									View
								</button>
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div>
		
		<!-- Skills Section -->
		<div class="flex-1 min-h-0">
			<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-6 text-center">Skills & Technologies</h2>
			<div class="grid grid-cols-4 md:grid-cols-6 lg:grid-cols-8 xl:grid-cols-10 gap-4 justify-items-center">
				{#each skills as skill}
					<div class="group flex flex-col items-center p-3 bg-white/70 dark:bg-gray-800/70 backdrop-blur-sm rounded-xl border border-gray-200/50 dark:border-gray-700/50 hover:shadow-lg hover:scale-105 transition-all duration-200">
						<img 
							src={skill.icon} 
							alt={skill.name}
							class="w-8 h-8 mb-2 group-hover:scale-110 transition-transform duration-200"
							on:error={(e) => {
								// Create a fallback icon with first letter
								const fallback = e.target.nextElementSibling;
								fallback.textContent = skill.name.charAt(0);
								fallback.style.display = 'flex';
								e.target.style.display = 'none';
							}}
						/>
						<div class="w-8 h-8 mb-2 bg-blue-500 text-white rounded-lg font-bold text-sm items-center justify-center hidden"></div>
						<span class="text-xs font-medium text-gray-700 dark:text-gray-300 text-center leading-tight">
							{skill.name}
						</span>
					</div>
				{/each}
			</div>
		</div>
	</div>
</div>

<style>
	:global(html, body) {
		scroll-behavior: smooth;
		overflow: hidden;
		height: 100%;
		font-family: 'Inter', sans-serif;
	}
	
	:global(.dark) {
		color-scheme: dark;
	}
	
	.font-serif {
		font-family: 'Crimson Text', serif;
	}
	
	.line-clamp-1 {
		display: -webkit-box;
		-webkit-line-clamp: 1;
		-webkit-box-orient: vertical;
		overflow: hidden;
	}
	
	.line-clamp-2 {
		display: -webkit-box;
		-webkit-line-clamp: 2;
		-webkit-box-orient: vertical;
		overflow: hidden;
	}
</style>