<!-- src/routes/projects/[id]/+page.svelte -->
<script lang="ts">
	import { page } from '$app/stores';
	import { onMount } from 'svelte';

	// Get project ID from URL
	$: projectId = $page.params.id ?? '';

	// Dark mode state
	let isDark = false;

	// Initialize dark mode on mount
	onMount(() => {
		const hour = new Date().getHours();
		const savedMode = localStorage.getItem('darkMode');
		isDark = savedMode ? JSON.parse(savedMode) : (hour >= 18 || hour <= 6);
		updateTheme();
	});

	// Update theme function
	function updateTheme() {
		if (typeof document !== 'undefined') {
			document.documentElement.classList.toggle('dark', isDark);
			document.body.classList.toggle('dark', isDark);
		}
	}

	// Toggle dark mode
	function toggleDarkMode() {
		isDark = !isDark;
		localStorage.setItem('darkMode', JSON.stringify(isDark));
		updateTheme();
	}

	// Project data
	const projects: Record<string, any> = {
		'1': {
			title: 'Cvelo',
			shortDescription: 'An AI job search platform that helps candidates move from job discovery to application with resume tailoring, cover letters, ATS scoring, tracking, and browser autofill.',
			fullDescription: 'Cvelo is a full-stack AI job search platform built to reduce friction between finding a job and actually applying to it well. The product combines resume parsing and rendering, AI-powered resume tailoring, cover letter generation, ATS scoring, job matching, application pipeline tracking, billing, browser push notifications, and a Chrome extension for autofilling external job boards. The architecture spans a React and Vite frontend, a FastAPI backend, PostgreSQL for core data, Redis with RQ workers for background jobs, object storage for uploads, and a Manifest V3 browser extension that supports embedded iframe ATS flows. The repository is set up like a production application, with health checks, Prometheus metrics, Sentry integration, Docker-based local development, environment-driven configuration, and clearly separated backend, frontend, deployment, and extension packages.',
			technologies: [
				'React 18',
				'Vite 5',
				'TypeScript',
				'FastAPI',
				'SQLAlchemy 2',
				'Alembic',
				'PostgreSQL 15',
				'Redis 7',
				'RQ Workers',
				'Chrome Extension (Manifest V3)',
				'OpenAI / Anthropic Abstraction',
				'Paystack',
				'Prometheus',
				'Sentry',
				'Docker Compose'
			],
			features: [
				'Resume upload, parsing, rendering, and management for multiple tailored variants',
				'AI-powered resume tailoring from job descriptions and guided cover letter generation',
				'ATS scoring and job matching to help candidates understand fit before applying',
				'Application pipeline with statuses, recent activity, and progress visibility',
				'Browser extension that autofills external job applications, including embedded iframe ATS flows',
				'Plan-aware billing with Paystack, usage gating, subscription flows, and unlock handling',
				'Browser push notifications for pipeline milestones and engagement events',
				'Production-focused API surface with auth, billing, templates, feedback, admin, and health endpoints'
			],
			challenges: [
				'Coordinating a multi-surface product across frontend, backend, workers, storage, and a Chrome extension',
				'Building reliable autofill for cross-frame and embedded ATS application flows',
				'Managing AI-powered document generation while enforcing billing plans and usage limits',
				'Supporting resilient apply flows with draft persistence, reload restoration, and post-billing return paths',
				'Operating a production-style stack with health checks, metrics, observability, and environment-based deployment'
			],
			github: 'https://github.com/horacenjoroge/Cvelo',
			liveDemo: 'https://cveloapp.com/',
			hideCode: true,
			highlights: [
				'End-to-end product covering discovery, document generation, application tracking, and external-job autofill',
				'Multi-package architecture: frontend, FastAPI backend, workers, deployment config, and Manifest V3 extension',
				'AI document workflows powered through provider abstraction and document-processing utilities',
				'Billing, notifications, and observability are built into the main product instead of treated as afterthoughts',
				'Live public deployment available at cveloapp.com'
			],
			productAreas: [
				{
					title: 'Resume System',
					description: 'Upload PDF and DOCX resumes, parse structured candidate data, manage default resumes, and create tailored variants per job.'
				},
				{
					title: 'Apply Flow',
					description: 'Guide users through resume tailoring, cover letter generation, draft persistence, and safe post-billing return flows.'
				},
				{
					title: 'Job Discovery',
					description: 'Surface matching roles, support fit analysis, and help candidates revisit promising opportunities.'
				},
				{
					title: 'Pipeline Tracking',
					description: 'Track movement across applied, screening, interview, offer, accepted, and rejected stages with recent activity visibility.'
				},
				{
					title: 'Browser Extension',
					description: 'Autofill external job applications, including embedded iframe ATS surfaces, with tracked session history and state transitions.'
				},
				{
					title: 'Billing and Notifications',
					description: 'Gate premium AI flows with Paystack-backed subscriptions and keep users engaged through browser push notifications.'
				}
			],
			architectureLayers: [
				'React + Vite + TypeScript frontend with dashboard, apply flow, billing, and job discovery experiences',
				'FastAPI backend handling auth, resumes, tailoring, cover letters, billing, feedback, templates, and admin flows',
				'PostgreSQL 15 for core platform data plus Redis and RQ for queues, caching, and background task execution',
				'Object storage for uploads and generated assets, with S3-compatible integrations',
				'Manifest V3 Chrome extension with content scripts, service worker, popup UI, and cross-frame autofill routing'
			],
			stackGroups: [
				{
					label: 'Frontend',
					items: ['React 18', 'Vite 5', 'TypeScript', 'React Router', 'Zustand', 'TipTap', 'PWA']
				},
				{
					label: 'Backend',
					items: ['FastAPI', 'SQLAlchemy 2', 'Alembic', 'PostgreSQL 15', 'Redis 7', 'RQ workers']
				},
				{
					label: 'AI and Docs',
					items: ['OpenAI / Anthropic abstraction', 'tiktoken', 'sentence-transformers', 'pdfplumber', 'python-docx', 'WeasyPrint']
				},
				{
					label: 'Platform',
					items: ['Paystack', 'pywebpush', 'Prometheus', 'Sentry', 'Docker Compose', 'Chrome Extension']
				}
			],
			apiAreas: [
				'/api/auth and /api/oauth for authentication and identity flows',
				'/api/ai, /api/resumes, /api/tailored, and /api/cover-letters for AI document workflows',
				'/api/job-tracker and /api/job-discovery for application management and matching',
				'/api/autofill for extension-assisted application support',
				'/api/billing, /api/subscription, and /api/paystack for monetization and entitlement control',
				'/api/push, /api/templates, /api/feedback, and /api/admin for engagement and platform operations'
			],
			devWorkflow: [
				'Clone the repo, copy `.env.example` to `.env`, and configure core auth, AI, billing, storage, and push keys',
				'Start the full local stack with `docker compose up --build` to launch postgres, redis, api, worker, and frontend',
				'Use `docker compose exec` workflows for migrations, worker inspection, test runs, and service-specific commands',
				'Build and load the browser extension from `packages/extension` when testing external application autofill flows',
				'Monitor reliability with `/api/health`, `/metrics`, structured logging, and Sentry-backed observability'
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

	$: project = projectId ? projects[projectId] : undefined;

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
					{#if !project.hideCode}
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
					{/if}
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

			{#if projectId === '1'}
				<div class="mb-16 grid grid-cols-1 md:grid-cols-3 gap-4">
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-blue-600 dark:text-blue-400 mb-2">Product Type</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">AI Job Search Platform</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Built around reducing friction from discovery to application.</p>
					</div>
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-emerald-600 dark:text-emerald-400 mb-2">Deployment Shape</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Multi-Surface System</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Frontend, API, workers, storage, billing, push, and extension all integrated.</p>
					</div>
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-orange-600 dark:text-orange-400 mb-2">Live Experience</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Production-Oriented</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Health checks, metrics, Sentry, billing, and extension workflows are all part of the repo.</p>
					</div>
				</div>

				<div class="mb-16 rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
					<div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
						<div>
							<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">Architecture Overview</h2>
							<p class="text-gray-700 dark:text-gray-300 leading-relaxed mb-6">
								Cvelo is organized like a production system rather than a single app repo. The frontend, API, queue workers, storage layer, billing logic, push notification flows, and browser extension each have clearly defined responsibilities and deployment concerns.
							</p>
							<div class="space-y-3">
								{#each project.architectureLayers as layer}
									<div class="flex items-start gap-3">
										<div class="mt-1 h-2.5 w-2.5 rounded-full bg-blue-500"></div>
										<p class="text-gray-700 dark:text-gray-300">{layer}</p>
									</div>
								{/each}
							</div>
						</div>
						<div>
							<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">Main Product Areas</h2>
							<div class="space-y-4">
								{#each project.productAreas as area}
									<div class="rounded-2xl bg-slate-50 dark:bg-gray-900/60 border border-slate-200 dark:border-gray-700 p-4">
										<h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">{area.title}</h3>
										<p class="text-sm leading-relaxed text-gray-600 dark:text-gray-400">{area.description}</p>
									</div>
								{/each}
							</div>
						</div>
					</div>
				</div>

				<div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-16">
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">Stack by Surface</h2>
						<div class="space-y-5">
							{#each project.stackGroups as group}
								<div>
									<h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-3">{group.label}</h3>
									<div class="flex flex-wrap gap-2">
										{#each group.items as item}
											<span class="rounded-full bg-slate-100 dark:bg-gray-900/70 border border-slate-200 dark:border-gray-700 px-3 py-1.5 text-sm text-gray-700 dark:text-gray-300">
												{item}
											</span>
										{/each}
									</div>
								</div>
							{/each}
						</div>
					</div>
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">API and Platform Surface</h2>
						<div class="space-y-3">
							{#each project.apiAreas as area}
								<div class="flex items-start gap-3 rounded-2xl bg-slate-50 dark:bg-gray-900/60 border border-slate-200 dark:border-gray-700 p-4">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-emerald-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{area}</p>
								</div>
							{/each}
						</div>
					</div>
				</div>

				<div class="mb-16 rounded-3xl bg-gradient-to-br from-slate-100 via-white to-blue-50 dark:from-gray-900 dark:via-gray-800 dark:to-slate-900 border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
					<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">Local Development and Operations</h2>
					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						{#each project.devWorkflow as step}
							<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5">
								<p class="text-gray-700 dark:text-gray-300 leading-relaxed">{step}</p>
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
					Feel free to try the live demo or reach out if you have any questions!
				</p>
				<div class="flex flex-wrap justify-center gap-4">
					{#if !project.hideCode}
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
					{/if}
					<a 
						href={project.liveDemo}
						target="_blank"
						class="inline-flex items-center px-6 py-3 bg-blue-600 hover:bg-blue-700 text-white rounded-lg font-medium transition-colors duration-200"
					>
						<svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"></path>
						</svg>
						Live Demo
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
	
</style>
