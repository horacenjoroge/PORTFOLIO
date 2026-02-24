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
			title: 'Provote',
			shortDescription: 'Voting and polling platform for secure, transparent decisions and community engagement.',
			fullDescription: 'Provote is a voting and polling platform designed for secure, transparent decisions and community engagement. Users can create and participate in polls and votes with clear results and auditability. The project provides a modern stack for building and running voting flows with a focus on reliability and user experience.',
			technologies: ['Node.js', 'TypeScript', 'React', 'PostgreSQL'],
			features: [
				'Create and manage polls and votes',
				'Secure, transparent voting and result visibility',
				'Community engagement and participation flows',
				'Modern web stack with TypeScript and React'
			],
			challenges: [
				'Ensuring vote integrity and preventing tampering',
				'Designing clear UX for creating and viewing polls',
				'Scaling for concurrent voters and real-time results'
			],
			github: 'https://github.com/horacenjoroge/provote',
			liveDemo: 'https://drive.google.com/file/d/1mVBfaW64q_juza02aIm0Y76ifX-jl38j/view?usp=sharing',
			highlights: [
				'Voting and polling platform for transparent decisions',
				'Secure, auditable results and community engagement',
				'TypeScript and React frontend with Node.js backend'
			]
		},
		'3': {
			title: 'AfricGraph',
			shortDescription: 'Ontology-driven decision platform for SMEs. FastAPI backend, React frontend, and supporting services run via Docker Compose.',
			fullDescription: 'AfricGraph is an ontology-driven decision platform for small and medium enterprises. The system combines a FastAPI backend with a React frontend and runs a full stack of services via Docker Compose: Neo4j for graph data, PostgreSQL, Redis, RabbitMQ, and Elasticsearch. It supports ingestion jobs via Celery workers, JWT authentication, and configurable CORS. Backend and frontend can be run together with docker-compose up, with API at port 8000, frontend at 3000, Neo4j Browser at 7474, and RabbitMQ management at 15672.',
			technologies: ['Python', 'FastAPI', 'React', 'TypeScript', 'Neo4j', 'PostgreSQL', 'Redis', 'RabbitMQ', 'Elasticsearch', 'Docker', 'Celery', 'Cypher'],
			features: [
				'Ontology-driven data model for SME decision support',
				'FastAPI backend with health checks and configurable env',
				'React frontend with TypeScript',
				'Neo4j graph database (7474, 7687)',
				'PostgreSQL, Redis, RabbitMQ, Elasticsearch in stack',
				'Celery workers for async ingestion jobs',
				'Docker Compose for local and production runs',
				'JWT authentication and CORS configuration'
			],
			challenges: [
				'Coordinating multiple data stores and message queues',
				'Designing ontology and graph schema for SME use cases',
				'Running and debugging ingestion pipeline with Celery',
				'Keeping Docker Compose and env config in sync across services'
			],
			github: 'https://github.com/horacenjoroge/AfricGraph',
			liveDemo: 'https://drive.google.com/file/d/1l9r45Qt9V5K-Aw0JpQqb6Ll7ZQtcGZR-/view?usp=sharing',
			highlights: [
				'Ontology-driven platform for SME decisions',
				'Full stack: FastAPI, React, Neo4j, PostgreSQL, Redis, RabbitMQ, Elasticsearch',
				'Single-command run with Docker Compose',
				'Celery-based ingestion pipeline with worker docs'
			]
		},
		'4': {
			title: 'Distributed-Event-Log-Platform',
			shortDescription: 'Production-ready distributed commit log system (Kafka/Pulsar-style) built from scratch, implementing principles from Designing Data-Intensive Applications.',
			fullDescription: 'DistributedLog is a production-ready distributed commit log system built from scratch in Python, implementing concepts from Martin Kleppmann\'s "Designing Data-Intensive Applications." It provides an append-only commit log with crash recovery, sparse offset indexing for O(log n) lookups, log compaction and retention, and producer/consumer clients with batching and compression. The system uses a multi-broker architecture over gRPC, leader-follower replication with In-Sync Replicas (ISR), and Raft consensus for leader election implemented from scratch. It supports exactly-once semantics via producer idempotence, distributed transactions (two-phase commit), and consumer isolation levels. Performance optimizations include zero-copy transfers (sendfile, mmap), async I/O for 10,000+ connections per thread, buffer pooling, and adaptive batch fetching. The project includes 38,120 lines of code across production code, tests, and documentation.',
			technologies: ['Python 3.10+', 'gRPC', 'Protocol Buffers', 'Raft', 'asyncio', 'pytest', 'Docker', 'Two-phase commit'],
			features: [
				'Append-only commit log with crash recovery and sparse offset indexing',
				'Producer/consumer clients with batching, compression, and topic partitioning',
				'Consumer groups with automatic rebalancing',
				'Multi-broker architecture with gRPC and leader-follower replication (ISR)',
				'Raft consensus for leader election and cluster controller',
				'Partition reassignment and live data migration',
				'Producer idempotence and distributed transactions (2PC)',
				'Zero-copy I/O, buffer pooling, and adaptive batch fetching'
			],
			challenges: [
				'Implementing Raft consensus and cluster controller from scratch',
				'Achieving exactly-once semantics across producers and consumers',
				'Designing zero-copy and async I/O for high throughput',
				'Coordinating multi-broker metadata and partition assignment'
			],
			github: 'https://github.com/horacenjoroge/Distributed-Event-Log-Platform',
			liveDemo: 'https://github.com/horacenjoroge/Distributed-Event-Log-Platform',
			highlights: [
				'Kafka/Pulsar-style distributed log built from scratch',
				'Raft consensus and ISR replication implemented in Python',
				'3x throughput and 10x concurrent connections with optimizations',
				'38,120 lines across production code, tests, and docs'
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

			<!-- Screenshots (only for projects 1 and 2) -->
			{#if project.screenshots && project.screenshots.length > 0 && (projectId === '1' || projectId === '2')}
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