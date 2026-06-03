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
			shortDescription: 'A backend-heavy voting platform with idempotent vote handling, API documentation, architecture diagrams, load testing, and production-oriented operations tooling.',
			fullDescription: 'Provote is a professional Django-based voting platform built around reliable vote handling, auditability, and operational readiness. The project exposes a REST API for polls, votes, users, and analytics; documents its surface with OpenAPI artifacts and extended API docs; and backs the platform with PostgreSQL, Redis, Celery, Docker, and Nginx. Beyond CRUD functionality, the repo shows serious backend engineering work: idempotent voting operations, real-time analytics, load testing, disaster recovery and backup scripts, security notes, monitoring setup, and comprehensive architecture documentation with Mermaid diagrams. It is a strong example of how to present a backend-first system even when the frontend is not the main story.',
			technologies: ['Python 3.11', 'Django 5', 'Django REST Framework', 'PostgreSQL 15', 'Redis 7', 'Celery', 'Gunicorn', 'Nginx', 'drf-spectacular', 'Docker Compose'],
			features: [
				'REST API for polls, votes, users, analytics, and related platform workflows',
				'Idempotent voting operations designed to prevent duplicate votes under retries and concurrency',
				'Published OpenAPI artifacts via `schema.json` and `schema.yml`, plus extended API documentation',
				'Insomnia collection for testing endpoints without building a custom frontend client',
				'Load-testing suite and supporting scripts for voting, websocket, and performance verification',
				'Operational scripts for backups, restore flows, safe migrations, and blue-green deployment support',
				'Comprehensive architecture and ERD documentation with Mermaid diagrams',
				'Docker-based environment with PostgreSQL, Redis, Celery, Gunicorn, and Nginx'
			],
			challenges: [
				'Designing vote creation so retries and concurrent requests remain safe and idempotent',
				'Coordinating database, cache, workers, and real-time infrastructure around a consistent voting workflow',
				'Documenting the system thoroughly enough that technical reviewers can understand architecture without a dedicated frontend demo',
				'Preparing the platform for operational concerns such as backup, restore, deployment, and monitoring'
			],
			exploreLinks: [
				{
					title: 'OpenAPI Schema',
					description: 'Inspect the machine-readable API contract committed in the repository.',
					url: 'https://github.com/horacenjoroge/AlxProjectNexus/blob/main/schema.yml'
				},
				{
					title: 'Insomnia Collection',
					description: 'Import the prepared API collection and exercise the endpoints without building a frontend.',
					url: 'https://github.com/horacenjoroge/AlxProjectNexus/blob/main/provote-insomnia-collection.json'
				},
				{
					title: 'API Reference',
					description: 'Read the curated API documentation covering the main backend surface.',
					url: 'https://github.com/horacenjoroge/AlxProjectNexus/blob/main/docs/api.md'
				},
				{
					title: 'Architecture Docs',
					description: 'Review the full system architecture, request flows, idempotency notes, and Mermaid diagrams.',
					url: 'https://github.com/horacenjoroge/AlxProjectNexus/blob/main/docs/architecture-comprehensive.md'
				},
				{
					title: 'Database ERD',
					description: 'See the schema design, relationships, constraints, and ERD-focused backend notes.',
					url: 'https://github.com/horacenjoroge/AlxProjectNexus/blob/main/docs/database-erd-design.md'
				},
				{
					title: 'Load Tests',
					description: 'Explore load and websocket test assets that validate reliability under traffic.',
					url: 'https://github.com/horacenjoroge/AlxProjectNexus/tree/main/load_tests'
				}
			],
			architectureSummary: [
				'Django REST Framework API behind Nginx and Gunicorn workers',
				'PostgreSQL for persistent state and Redis for cache, broker, and pub/sub',
				'Celery workers and Celery Beat handling background and scheduled tasks',
				'Django Channels and Redis pub/sub for real-time updates',
				'Documented request flow, idempotency path, ERD, and scaling strategy in Mermaid-backed architecture docs'
			],
			apiShowcase: [
				'Poll endpoints for listing, creating, retrieving, and viewing poll results',
				'Vote endpoints designed around idempotent creation and safe retry behavior',
				'User and analytics endpoints for platform visibility and reporting',
				'OpenAPI schema artifacts committed for tooling, validation, and client exploration'
			],
			opsShowcase: [
				'`run_load_test.sh` and the `load_tests/` suite for backend and websocket performance checks',
				'Backup, restore, and backup-verification scripts in `scripts/`',
				'Safe migration and blue-green deployment support scripts',
				'Monitoring and disaster-recovery documentation for production-style operations'
			],
			systemTopics: [
				'Idempotency design for write-heavy APIs',
				'Concurrency control and safe retry handling',
				'Caching and background processing with Redis and Celery',
				'Real-time update architecture and websocket scaling',
				'Operational readiness through monitoring, recovery, and scripted workflows'
			],
			availabilityNotes: [
				'Swagger/OpenAPI artifacts are clearly available in the repo through `schema.json` and `schema.yml`',
				'An importable API client collection is available through the Insomnia export',
				'Mermaid diagrams are already written in the architecture documentation and can be surfaced in the portfolio narrative',
				'Load-test and operations scripts are available for demonstration of reliability and deployment maturity',
				'A dedicated seed-data or demo-data workflow was not obvious from the current repo surface, so the portfolio should avoid claiming it exists until we verify or add it'
			],
			github: 'https://github.com/horacenjoroge/provote',
			liveDemo: 'https://drive.google.com/file/d/1mVBfaW64q_juza02aIm0Y76ifX-jl38j/view?usp=sharing',
			highlights: [
				'Strong backend showcase built around documented APIs, architecture diagrams, and operational tooling',
				'Idempotent vote handling and load testing make the system story stronger than a simple CRUD demo',
				'OpenAPI schema, Insomnia collection, and backend docs make the project explorable without a full custom frontend',
				'Production-minded setup with Docker, Redis, Celery, monitoring notes, and deployment scripts'
			]
		},
		'3': {
			title: 'AfricGraph',
			shortDescription: 'Ontology-driven SME intelligence platform with graph-first modeling, documented REST and GraphQL surfaces, monitoring assets, seed data, and deployment tooling shaped by Designing Data-Intensive Applications.',
			fullDescription: 'AfricGraph is an ontology-driven decision platform for small and medium enterprises that models businesses, people, suppliers, customers, payments, invoices, and transactions as a knowledge graph. The system combines a FastAPI backend with a React frontend and runs a full service stack through Docker Compose: Neo4j for graph relationships, PostgreSQL for metadata and workflow state, Redis and RabbitMQ for supporting infrastructure, Celery workers for ingestion jobs, Elasticsearch for search, and monitoring assets for observability. The repo also includes interactive API documentation, GraphQL schema support, ERD documentation spanning both relational and graph structures, deployment runbooks, health checks, Prometheus and Grafana monitoring configuration, plus seed and sample data for realistic testing. This project was strongly shaped by my reading of Martin Kleppmann\'s "Designing Data-Intensive Applications," especially the parts about choosing the right data model for the problem, coordinating multiple storage systems, and designing services that move data reliably between queues, databases, search, and graph stores.',
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
			bookInspiration: 'This project grew out of ideas from "Designing Data-Intensive Applications" by Martin Kleppmann, especially the tradeoffs around data models, asynchronous processing, and system boundaries.',
			learnedTopics: [
				'How graph databases and relational databases solve different access-pattern problems, and when to combine them in one system',
				'How message brokers and worker queues help decouple ingestion, background processing, and user-facing request paths',
				'How to think about consistency, indexing, and data flow when multiple stores such as Neo4j, PostgreSQL, Redis, and Elasticsearch coexist',
				'How distributed application complexity shows up in deployment, configuration, health checks, and observability long before production scale'
			],
			exploreLinks: [
				{
					title: 'OpenAPI Guide',
					description: 'Interactive Swagger, ReDoc, and raw `openapi.json` usage are documented for the REST API.',
					url: 'https://github.com/horacenjoroge/AfricGraph/blob/master/docs/openapi-guide.md'
				},
				{
					title: 'ERD and Data Model',
					description: 'Detailed schema notes covering both PostgreSQL tables and Neo4j graph structure.',
					url: 'https://github.com/horacenjoroge/AfricGraph/blob/master/docs/erd.md'
				},
				{
					title: 'Docs Index',
					description: 'Start from the documentation hub for architecture, API reference, GraphQL schema, deployment, and runbooks.',
					url: 'https://github.com/horacenjoroge/AfricGraph/blob/master/docs/README.md'
				},
				{
					title: 'Monitoring Setup',
					description: 'Prometheus metrics, Grafana dashboards, and alerting configuration for platform observability.',
					url: 'https://github.com/horacenjoroge/AfricGraph/blob/master/backend/monitoring/README.md'
				},
				{
					title: 'Seed and Sample Data',
					description: 'Seed the platform for testing with `seed_data.py` and inspect the provided `sample_graph_data.json` asset.',
					url: 'https://github.com/horacenjoroge/AfricGraph/blob/master/backend/scripts/seed_data.py'
				},
				{
					title: 'Deployment Tooling',
					description: 'Health checks, restore flows, rollback support, and deployment scripts are part of the repo.',
					url: 'https://github.com/horacenjoroge/AfricGraph/tree/master/deployment/scripts'
				}
			],
			architectureSummary: [
				'FastAPI backend and React frontend running alongside Neo4j, PostgreSQL, Redis, RabbitMQ, Elasticsearch, and Celery workers',
				'Graph-first domain model for entity relationships, supported by PostgreSQL for metadata, workflow state, and audit data',
				'Interactive REST docs at `/docs` and `/redoc`, plus GraphQL exploration through `/graphql`',
				'Health and metrics endpoints exposed for platform visibility, with Prometheus and Grafana assets committed in the repo',
				'Deployment scripts and Docker Compose setup designed to make the full multi-service platform reproducible locally'
			],
			apiShowcase: [
				'Swagger UI at `/docs`, ReDoc at `/redoc`, and raw OpenAPI schema at `/openapi.json`',
				'GraphQL schema and explorer support for graph-oriented access patterns',
				'REST endpoint groups covering businesses, risk, fraud, graph operations, search, workflows, backup, and auth',
				'Client-generation workflows documented through the OpenAPI guide'
			],
			opsShowcase: [
				'Prometheus metrics at `/metrics` with Grafana dashboards and alert definitions committed in the repo',
				'Health-check scripts spanning backend, frontend, PostgreSQL, Neo4j, Redis, and Elasticsearch',
				'Deployment helper scripts for deploy, update, rollback, and restore workflows',
				'Monitoring and recovery documentation in `backend/monitoring/README.md`, `deployment/README.md`, and disaster-recovery assets'
			],
			availabilityNotes: [
				'Interactive API documentation is clearly available through Swagger, ReDoc, and raw OpenAPI endpoints',
				'The repo documents both REST and GraphQL surfaces, which makes the backend story richer than a single API style',
				'Seed/sample data are genuinely present through `backend/scripts/seed_data.py` and `sample_graph_data.json`',
				'Monitoring assets are already committed, including Prometheus config, Grafana dashboards, and alert definitions',
				'ERD and ontology-oriented documentation already exist, so the portfolio can confidently point to real system-design artifacts instead of vague claims'
			],
			github: 'https://github.com/horacenjoroge/AfricGraph',
			liveDemo: 'https://drive.google.com/file/d/1l9r45Qt9V5K-Aw0JpQqb6Ll7ZQtcGZR-/view?usp=sharing',
			highlights: [
				'Ontology-driven platform for SME decisions',
				'Full stack: FastAPI, React, Neo4j, PostgreSQL, Redis, RabbitMQ, Elasticsearch',
				'Single-command run with Docker Compose',
				'Celery-based ingestion pipeline with worker docs',
				'Built as a practical extension of lessons from Designing Data-Intensive Applications'
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
			bookInspiration: 'This project was a direct result of reading "Designing Data-Intensive Applications" by Martin Kleppmann and then trying to implement the core ideas in a real distributed log system.',
			learnedTopics: [
				'How append-only logs, segment indexing, compaction, and retention policies work as the foundation of event-driven systems',
				'How replication, leader election, ISR management, and consensus algorithms such as Raft shape fault-tolerant distributed systems',
				'How exactly-once semantics, idempotent producers, and transactional workflows become much harder in real multi-broker environments',
				'How batching, zero-copy I/O, async networking, and partitioning strategy affect throughput, latency, and operational behavior'
			],
			github: 'https://github.com/horacenjoroge/Distributed-Event-Log-Platform',
			liveDemo: 'https://github.com/horacenjoroge/Distributed-Event-Log-Platform',
			highlights: [
				'Kafka/Pulsar-style distributed log built from scratch',
				'Raft consensus and ISR replication implemented in Python',
				'3x throughput and 10x concurrent connections with optimizations',
				'38,120 lines across production code, tests, and docs',
				'A hands-on implementation of concepts studied in Designing Data-Intensive Applications'
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

			{#if projectId === '2'}
				<div class="mb-16 grid grid-cols-1 md:grid-cols-3 gap-4">
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-blue-600 dark:text-blue-400 mb-2">API Surface</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Documented Backend</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">OpenAPI schema files, API docs, and an Insomnia collection are already present in the repo.</p>
					</div>
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-emerald-600 dark:text-emerald-400 mb-2">System Design</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Explained in Depth</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Architecture, ERD, API flows, and idempotency behavior are written out in long-form docs with Mermaid diagrams.</p>
					</div>
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-orange-600 dark:text-orange-400 mb-2">Ops Readiness</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Beyond CRUD</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Load tests, backup scripts, restore workflows, and deployment helpers make the backend story much stronger.</p>
					</div>
				</div>

				<div class="mb-16 rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
					<div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
						<div>
							<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">Explore the Backend</h2>
							<div class="grid grid-cols-1 gap-4">
								{#each project.exploreLinks as link}
									<a
										href={link.url}
										target="_blank"
										class="rounded-2xl bg-slate-50 dark:bg-gray-900/60 border border-slate-200 dark:border-gray-700 p-4 hover:border-blue-400 dark:hover:border-blue-500 transition-colors duration-200"
									>
										<div class="flex items-start justify-between gap-4">
											<div>
												<h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">{link.title}</h3>
												<p class="text-sm leading-relaxed text-gray-600 dark:text-gray-400">{link.description}</p>
											</div>
											<svg class="w-5 h-5 text-blue-600 dark:text-blue-400 flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 4h6m0 0v6m0-6L10 14M5 8v11h11"></path>
											</svg>
										</div>
									</a>
								{/each}
							</div>
						</div>
						<div>
							<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">Core Systems Topics</h2>
							<div class="space-y-4">
								{#each project.systemTopics as topic}
									<div class="rounded-2xl bg-slate-50 dark:bg-gray-900/60 border border-slate-200 dark:border-gray-700 p-4">
										<p class="text-sm leading-relaxed text-gray-700 dark:text-gray-300">{topic}</p>
									</div>
								{/each}
							</div>
						</div>
					</div>
				</div>

				<div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-16">
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-5">Architecture Snapshot</h2>
						<div class="space-y-3">
							{#each project.architectureSummary as item}
								<div class="flex items-start gap-3">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-blue-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{item}</p>
								</div>
							{/each}
						</div>
					</div>
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-5">API Surface</h2>
						<div class="space-y-3">
							{#each project.apiShowcase as item}
								<div class="flex items-start gap-3">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-emerald-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{item}</p>
								</div>
							{/each}
						</div>
					</div>
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-5">Ops and Reliability</h2>
						<div class="space-y-3">
							{#each project.opsShowcase as item}
								<div class="flex items-start gap-3">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-orange-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{item}</p>
								</div>
							{/each}
						</div>
					</div>
				</div>

				<div class="mb-16 rounded-3xl bg-gradient-to-br from-slate-100 via-white to-emerald-50 dark:from-gray-900 dark:via-gray-800 dark:to-slate-900 border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
					<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">What Is Ready To Showcase</h2>
					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						{#each project.availabilityNotes as note}
							<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5">
								<p class="text-gray-700 dark:text-gray-300 leading-relaxed">{note}</p>
							</div>
						{/each}
					</div>
				</div>
			{/if}

			{#if projectId === '3'}
				<div class="mb-16 grid grid-cols-1 md:grid-cols-3 gap-4">
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-blue-600 dark:text-blue-400 mb-2">Data Model</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Graph + Relational</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Neo4j handles relationship-heavy intelligence while PostgreSQL carries metadata, audit, and workflow state.</p>
					</div>
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-emerald-600 dark:text-emerald-400 mb-2">Backend Surface</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">REST + GraphQL</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Swagger, ReDoc, GraphQL schema support, and client-generation docs are all part of the project surface.</p>
					</div>
					<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5 shadow-lg">
						<p class="text-sm uppercase tracking-[0.2em] text-orange-600 dark:text-orange-400 mb-2">Operations</p>
						<h3 class="text-xl font-semibold text-gray-900 dark:text-white">Observable and Runnable</h3>
						<p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Health checks, metrics, dashboards, deployment scripts, and recovery assets make the system demonstrably operational.</p>
					</div>
				</div>

				<div class="mb-16 rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
					<div class="grid grid-cols-1 lg:grid-cols-2 gap-10">
						<div>
							<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">Explore the Backend</h2>
							<div class="grid grid-cols-1 gap-4">
								{#each project.exploreLinks as link}
									<a
										href={link.url}
										target="_blank"
										class="rounded-2xl bg-slate-50 dark:bg-gray-900/60 border border-slate-200 dark:border-gray-700 p-4 hover:border-blue-400 dark:hover:border-blue-500 transition-colors duration-200"
									>
										<div class="flex items-start justify-between gap-4">
											<div>
												<h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">{link.title}</h3>
												<p class="text-sm leading-relaxed text-gray-600 dark:text-gray-400">{link.description}</p>
											</div>
											<svg class="w-5 h-5 text-blue-600 dark:text-blue-400 flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
												<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 4h6m0 0v6m0-6L10 14M5 8v11h11"></path>
											</svg>
										</div>
									</a>
								{/each}
							</div>
						</div>
						<div>
							<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-4">What I Learned</h2>
							<div class="space-y-4">
								{#each project.learnedTopics as topic}
									<div class="rounded-2xl bg-slate-50 dark:bg-gray-900/60 border border-slate-200 dark:border-gray-700 p-4">
										<p class="text-sm leading-relaxed text-gray-700 dark:text-gray-300">{topic}</p>
									</div>
								{/each}
							</div>
						</div>
					</div>
				</div>

				<div class="grid grid-cols-1 lg:grid-cols-3 gap-8 mb-16">
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-5">Architecture Snapshot</h2>
						<div class="space-y-3">
							{#each project.architectureSummary as item}
								<div class="flex items-start gap-3">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-blue-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{item}</p>
								</div>
							{/each}
						</div>
					</div>
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-5">API Surface</h2>
						<div class="space-y-3">
							{#each project.apiShowcase as item}
								<div class="flex items-start gap-3">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-emerald-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{item}</p>
								</div>
							{/each}
						</div>
					</div>
					<div class="rounded-3xl bg-white/75 dark:bg-gray-800/70 backdrop-blur-sm border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
						<h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-5">Ops and Reliability</h2>
						<div class="space-y-3">
							{#each project.opsShowcase as item}
								<div class="flex items-start gap-3">
									<div class="mt-1 h-2.5 w-2.5 rounded-full bg-orange-500"></div>
									<p class="text-gray-700 dark:text-gray-300">{item}</p>
								</div>
							{/each}
						</div>
					</div>
				</div>

				<div class="mb-16 rounded-3xl bg-gradient-to-br from-slate-100 via-white to-cyan-50 dark:from-gray-900 dark:via-gray-800 dark:to-slate-900 border border-gray-200/60 dark:border-gray-700/60 p-8 shadow-xl">
					<h2 class="text-3xl font-bold text-gray-900 dark:text-white mb-6">What Is Ready To Showcase</h2>
					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						{#each project.availabilityNotes as note}
							<div class="rounded-2xl bg-white/80 dark:bg-gray-800/80 border border-gray-200/60 dark:border-gray-700/60 p-5">
								<p class="text-gray-700 dark:text-gray-300 leading-relaxed">{note}</p>
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

					{#if project.bookInspiration}
						<div class="mt-8 rounded-2xl bg-blue-50 dark:bg-blue-950/30 border border-blue-200/70 dark:border-blue-900/70 p-5">
							<h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-3">Book Influence</h3>
							<p class="text-gray-700 dark:text-gray-300 leading-relaxed">
								{project.bookInspiration}
							</p>
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

					{#if project.learnedTopics}
						<div>
							<h3 class="text-2xl font-bold text-gray-900 dark:text-white mb-4">What I Learned</h3>
							<ul class="space-y-2">
								{#each project.learnedTopics as topic}
									<li class="flex items-start">
										<svg class="w-5 h-5 text-blue-500 mr-3 mt-0.5 flex-shrink-0" fill="currentColor" viewBox="0 0 20 20">
											<path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v4a1 1 0 102 0V7zm-1 8a1.5 1.5 0 100-3 1.5 1.5 0 000 3z" clip-rule="evenodd"></path>
										</svg>
										<span class="text-gray-700 dark:text-gray-300">{topic}</span>
									</li>
								{/each}
							</ul>
						</div>
					{/if}
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
