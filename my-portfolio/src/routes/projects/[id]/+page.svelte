<!-- src/routes/projects/[id]/+page.svelte -->
<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	// Get project ID from URL
	$: projectId = $page.params.id;

	// Dark mode state
	let isDark = false;

	// Initialize dark mode on mount
	onMount(() => {
		const hour = new Date().getHours();
		isDark = hour >= 18 || hour <= 6;
		updateTheme();
	});

	// Update theme function
	function updateTheme() {
		if (typeof document !== 'undefined') {
			if (isDark) {
				document.documentElement.classList.add('dark');
				document.body.classList.add('dark');
			} else {
				document.documentElement.classList.remove('dark');
				document.body.classList.remove('dark');
			}
		}
	}

	// Toggle dark mode
	function toggleDarkMode() {
		isDark = !isDark;
		updateTheme();
	}

	// Project data
	const projects = {
		'1': {
			title: 'Trainly - Your Personal Fitness Companion',
			shortDescription: 'A comprehensive fitness tracking mobile application built with React Native. Combines workout tracking, social features, and progress analytics to create a complete fitness ecosystem.',
			fullDescription: 'Trainly is a comprehensive fitness tracking mobile application built with React Native that combines workout tracking, social features, and emergency safety features to create a complete fitness ecosystem for users. The app features real-time workout tracking for multiple activity types including running, cycling, swimming, and gym workouts. It includes GPS route tracking, performance metrics like distance, pace, speed, calories, and heart rate monitoring. Key social features include the ability to share workouts, connect with friends, participate in a community feed, and celebrate achievements together. The app also prioritizes user safety with emergency contacts, SOS functionality, and planned fall detection features.',
			technologies: ['React Native 0.79.4', 'Expo 53.0.0', 'Node.js 18+', 'MongoDB Atlas', 'React Navigation', 'React Native Maps', 'Express.js', 'JWT', 'AsyncStorage', 'Railway'],
			features: [
				'Real-time workout tracking for multiple activity types',
				'GPS route tracking and mapping',
				'Performance metrics tracking (distance, pace, calories)',
				'Social fitness community with posts and connections',
				'Emergency safety features with SOS functionality',
				'Progress dashboard with visual analytics',
				'Achievement system with badges and milestones',
				'Dark/Light theme customization',
				'Offline support with cloud synchronization',
				'Cross-platform support (Android & iOS ready)'
			],
			challenges: [
				'Implementing accurate GPS tracking and route mapping',
				'Managing offline data synchronization',
				'Optimizing battery usage for continuous tracking',
				'Creating responsive cross-platform UI components',
				'Integrating emergency safety features reliably'
			],
			github: 'https://github.com/horacenjoroge/trainly',
			liveDemo: 'https://drive.google.com/file/d/1MJpB_6pGK1YWRBUoOseVetiPOH1WmMRE/view?usp=sharing',
			screenshots: [
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/trainly/Profile.jpeg',
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/trainly/Home.jpeg',
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/trainly/Sign%20In.jpeg',
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/trainly/Training.jpeg'
			],
			highlights: [
				'102MB APK with comprehensive fitness tracking',
				'Real-time GPS tracking and route visualization',
				'Social fitness community features',
				'Emergency SOS functionality for safety',
				'Cross-platform React Native development'
			]
		},
		'2': {
			title: 'Event Ticketing Platform',
			shortDescription: 'A comprehensive, production-ready event ticketing platform built with microservices architecture, featuring automated CI/CD, load balancing, and enterprise-grade monitoring.',
			fullDescription: 'This event ticketing platform represents enterprise-grade microservices architecture with 7 independent services including user management, event management, ticket inventory, order processing, payment integration, and notifications. The platform handles high-traffic scenarios with real-time ticket inventory management, distributed order processing using saga patterns, and multi-provider payment integration including Stripe, M-Pesa, and Flutterwave. Built with comprehensive DevOps practices including automated CI/CD pipelines, blue-green deployments, load balancing with Nginx, and enterprise monitoring with Prometheus and Grafana. The system has been load tested to handle 283 requests/second with 100% success rate.',
			technologies: ['NestJS', 'TypeScript', 'PostgreSQL 15', 'Prisma ORM', 'Docker', 'Kubernetes', 'RabbitMQ', 'Redis', 'Nginx', 'Prometheus', 'Grafana', 'GitHub Actions'],
			features: [
				'Microservices architecture with 7 independent services',
				'Real-time ticket inventory with reservation system',
				'Multi-provider payment processing (Stripe, M-Pesa, Flutterwave)',
				'Event-driven communication with RabbitMQ',
				'Load balancing with Nginx and health monitoring',
				'Comprehensive CI/CD pipeline with automated testing',
				'Blue-green deployment strategy for zero downtime',
				'Enterprise monitoring with Prometheus and Grafana',
				'Role-based access control for different user types',
				'Distributed transaction management with saga pattern'
			],
			challenges: [
				'Designing microservices boundaries and communication patterns',
				'Implementing distributed transaction management',
				'Achieving high availability with load balancing',
				'Setting up comprehensive monitoring and alerting',
				'Managing database consistency across services'
			],
			github: 'https://github.com/horacenjoroge/Event-ticketing-backend',
			liveDemo: 'https://event-ticketing-demo.railway.app',
			screenshots: [
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/prometheus%20and%20grafana/Screenshot%202025-07-30%20at%2021.54.44.png',
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/prometheus%20and%20grafana/Screenshot%202025-07-31%20at%2003.52.11.png',
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/prometheus%20and%20grafana/Screenshot%202025-07-31%20at%2004.09.26.png',
				'https://raw.githubusercontent.com/horacenjoroge/project-images/main/prometheus%20and%20grafana/Screenshot%202025-07-31%20at%2004.56.13.png'
			],
			highlights: [
				'283 requests/second throughput with 100% success rate',
				'Zero-downtime deployments with blue-green strategy',
				'Comprehensive monitoring with Prometheus/Grafana',
				'Multi-provider payment integration',
				'Enterprise-grade microservices architecture'
			]
		},
		'3': {
			title: 'E-commerce API',
			shortDescription: 'RESTful API with payment processing and inventory management',
			fullDescription: 'A comprehensive e-commerce REST API built with TypeScript and Express, featuring complete product management, user authentication, shopping cart functionality, and payment processing integration. The API follows RESTful principles and includes advanced features like inventory tracking, order management, user reviews, and analytics. It is designed with scalability and security in mind, implementing proper error handling, input validation, and rate limiting. The system includes automated testing, API documentation with Swagger, and deployment configurations for cloud platforms.',
			technologies: ['TypeScript', 'Express', 'MongoDB', 'Mongoose', 'Stripe', 'JWT', 'Swagger', 'Jest'],
			features: [
				'Complete user authentication system',
				'Product catalog with categories and search',
				'Shopping cart and wishlist functionality',
				'Order processing and tracking',
				'Payment integration with Stripe',
				'Inventory management',
				'User reviews and ratings',
				'Admin dashboard API endpoints'
			],
			challenges: [
				'Designing scalable database schemas',
				'Implementing secure payment processing',
				'Managing inventory across concurrent orders',
				'Creating comprehensive API documentation'
			],
			github: 'https://github.com/yourusername/ecommerce-api',
			liveDemo: 'https://ecommerce-api-docs.vercel.app',
			screenshots: [
				'https://images.unsplash.com/photo-1556742049-0cfed4f6a45d?w=800&h=600',
				'https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800&h=600'
			],
			highlights: [
				'RESTful API design with comprehensive documentation',
				'Secure payment processing with Stripe integration',
				'Scalable database schema with MongoDB',
				'Automated testing and API documentation'
			]
		},
		'4': {
			title: 'Task Management Application',
			shortDescription: 'Productivity app with drag-and-drop functionality',
			fullDescription: 'A modern task management application built with React, featuring an intuitive drag-and-drop interface, project organization, and team collaboration tools. The app helps users organize tasks, track progress, and collaborate effectively. The application includes features like task prioritization, due date tracking, file attachments, and real-time collaboration. It is designed with a focus on user experience and productivity enhancement. Built with modern React patterns including hooks, context API, and optimized for performance with code splitting and lazy loading.',
			technologies: ['React', 'Node.js', 'PostgreSQL', 'Socket.io', 'React DnD', 'Material-UI', 'JWT'],
			features: [
				'Drag-and-drop task organization',
				'Project and board management',
				'Task prioritization and labeling',
				'Due date tracking and notifications',
				'File attachments and comments',
				'Team collaboration and sharing',
				'Real-time updates',
				'Progress tracking and analytics'
			],
			challenges: [
				'Implementing smooth drag-and-drop interactions',
				'Managing complex state with multiple boards',
				'Optimizing real-time collaboration',
				'Creating an intuitive user interface'
			],
			github: 'https://github.com/yourusername/task-app',
			liveDemo: 'https://task-management-demo.vercel.app',
			screenshots: [
				'https://images.unsplash.com/photo-1611224923853-80b023f02d71?w=800&h=600',
				'https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?w=800&h=600'
			],
			highlights: [
				'Smooth drag-and-drop interface with React DnD',
				'Real-time collaboration with Socket.io',
				'Modern React architecture with hooks',
				'Responsive design for all devices'
			]
		}
	};

	$: project = projects[projectId];

	function goBack() {
		window.history.back();
	}
</script>

<svelte:head>
	<title>{project?.title || 'Project'} - Horace Njoroge</title>
	<meta name="description" content={project?.shortDescription || 'Project details'} />
	<link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700&family=Lora:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
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

{#if project}
	<div class="min-h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100 dark:from-gray-900 dark:via-gray-800 dark:to-gray-900 transition-all duration-500">
		<div class="max-w-6xl mx-auto px-6 py-8">
			<!-- Back Button -->
			<button 
				on:click={goBack}
				class="inline-flex items-center mb-8 px-4 py-2 bg-white dark:bg-gray-800 border border-gray-300 dark:border-gray-600 rounded-lg hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors duration-200"
			>
				<svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
				</svg>
				Back to Portfolio
			</button>

			<!-- Project Header -->
			<div class="text-center mb-12">
				<h1 class="text-4xl lg:text-5xl font-bold text-gray-900 dark:text-white mb-4">
					{project.title}
				</h1>
				<p class="text-xl text-gray-600 dark:text-gray-400 mb-8 max-w-3xl mx-auto">
					{project.shortDescription}
				</p>

				<!-- Action Buttons -->
				<div class="flex flex-wrap justify-center gap-4 mb-8">
					<a 
						href={project.github}
						target="_blank"
						class="inline-flex items-center px-6 py-3 bg-gray-900 dark:bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-600 text-white rounded-lg font-medium transition-colors duration-200 shadow-md"
					>
						<svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20">
							<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"></path>
						</svg>
						View Code
					</a>
					<a 
						href={project.liveDemo}
						target="_blank"
						class="inline-flex items-center px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition-colors duration-200 shadow-md"
					>
						<svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
						</svg>
						Live Demo
					</a>
				</div>

				<!-- Technologies -->
				<div class="flex flex-wrap justify-center gap-2">
					{#each project.technologies as tech}
						<span class="bg-white/70 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/50 dark:border-gray-700/50 px-3 py-1.5 rounded-full text-sm font-medium text-gray-700 dark:text-gray-300">
							{tech}
						</span>
					{/each}
				</div>
			</div>

			<!-- Screenshots -->
			{#if project.screenshots && project.screenshots.length > 0}
				<div class="mb-16">
					<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-8 text-center">Screenshots</h2>
					<div class="grid grid-cols-1 md:grid-cols-2 gap-6">
						{#each project.screenshots as screenshot, index}
							<div class="bg-white dark:bg-gray-800 rounded-xl p-4 shadow-lg">
								<img 
									src={screenshot} 
									alt={`${project.title} screenshot ${index + 1}`}
									class="w-full h-64 object-cover rounded-lg"
								/>
							</div>
						{/each}
					</div>
				</div>
			{/if}

			<!-- Project Details Grid -->
			<div class="grid grid-cols-1 lg:grid-cols-2 gap-12 mb-16">
				<!-- Description -->
				<div>
					<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">Project Overview</h2>
					<p class="text-gray-700 dark:text-gray-300 leading-relaxed mb-6">
						{project.fullDescription}
					</p>

					<!-- Project Highlights -->
					{#if project.highlights}
						<div class="mt-8">
							<h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">Key Highlights</h3>
							<div class="space-y-2">
								{#each project.highlights as highlight}
									<div class="flex items-start">
										<svg class="w-5 h-5 text-blue-500 mr-3 mt-0.5 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
											<path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path>
										</svg>
										<span class="text-gray-700 dark:text-gray-300 font-medium">{highlight}</span>
									</div>
								{/each}
							</div>
						</div>
					{/if}
				</div>

				<!-- Features & Challenges -->
				<div class="space-y-8">
					<!-- Features -->
					<div>
						<h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">Key Features</h3>
						<ul class="space-y-2">
							{#each project.features as feature}
								<li class="flex items-start">
									<svg class="w-5 h-5 text-green-500 mr-3 mt-0.5 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
										<path fill-rule="evenodd" d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z" clip-rule="evenodd"></path>
									</svg>
									<span class="text-gray-700 dark:text-gray-300">{feature}</span>
								</li>
							{/each}
						</ul>
					</div>

					<!-- Challenges -->
					<div>
						<h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">Technical Challenges</h3>
						<ul class="space-y-2">
							{#each project.challenges as challenge}
								<li class="flex items-start">
									<svg class="w-5 h-5 text-orange-500 mr-3 mt-0.5 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
										<path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd"></path>
									</svg>
									<span class="text-gray-700 dark:text-gray-300">{challenge}</span>
								</li>
							{/each}
						</ul>
					</div>
				</div>
			</div>

			<!-- Call to Action -->
			<div class="text-center bg-white/70 dark:bg-gray-800/70 backdrop-blur-sm rounded-2xl p-8 border border-gray-200/50 dark:border-gray-700/50">
				<h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">Interested in this project?</h3>
				<p class="text-gray-600 dark:text-gray-400 mb-6">
					Feel free to explore the code, try the live demo, or reach out if you have any questions!
				</p>
				<div class="flex flex-wrap justify-center gap-4">
					<a 
						href={project.github}
						target="_blank"
						class="inline-flex items-center px-6 py-3 bg-gray-900 dark:bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-600 text-white rounded-lg font-medium transition-colors duration-200"
					>
						<svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20">
							<path fill-rule="evenodd" d="M10 0C4.477 0 0 4.484 0 10.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0110 4.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.203 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.942.359.31.678.921.678 1.856 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0020 10.017C20 4.484 15.522 0 10 0z" clip-rule="evenodd"></path>
						</svg>
						Explore Code
					</a>
					<button 
						on:click={goBack}
						class="inline-flex items-center px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition-colors duration-200"
					>
						<svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
						</svg>
						Back to Portfolio
					</button>
				</div>
			</div>
		</div>
	</div>
{:else}
	<!-- Project Not Found -->
	<div class="min-h-screen bg-gradient-to-br from-slate-50 via-white to-slate-100 dark:from-gray-900 dark:via-gray-800 dark:to-gray-900 flex items-center justify-center">
		<div class="text-center">
			<h1 class="text-4xl font-bold text-gray-900 dark:text-white mb-4">Project Not Found</h1>
			<p class="text-gray-600 dark:text-gray-400 mb-8">The project you're looking for doesn't exist.</p>
			<button 
				on:click={goBack}
				class="inline-flex items-center px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition-colors duration-200"
			>
				<svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
				</svg>
				Back to Portfolio
			</button>
		</div>
	</div>
{/if}

<style>
	:global(html, body) {
		scroll-behavior: smooth;
		font-family: 'Outfit', -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
	}
	
	:global(.dark) {
		color-scheme: dark;
	}
	
	.font-serif {
		font-family: 'Lora', Georgia, 'Times New Roman', serif;
	}
</style>