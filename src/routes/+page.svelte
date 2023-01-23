<script lang="ts">
	import { spring } from 'svelte/motion';
	import { flip } from 'svelte/animate';
	import Langicon from '../components/langicon.svelte';
	import ProjectCard from '../components/project_card.svelte';
	import EducationCard from '../components/education_card.svelte';

	function sleep(ms: number) {
		return new Promise((resolve) => setTimeout(resolve, ms));
	}

	let sectionsOpacity = spring([1, 0.3, 0.3, 0.3, 0.3]);
	let copyBannerOpacity = spring(0);
	let icons: Array<string> = [
		'c.png',
		'rust.png',
		'node.png',
		'django.png',
		'react.png',
		'python.png',
		'tensorflow.png',
		'opencv.webp'
	];

	// @ts-ignore
	let intersectionObserver;

	const ioConfiguration = {
		rootMargin: '-50% 0% -50% 0%',
		threshold: 0
	};

	function ensureIntersectionObserver() {
		// @ts-ignore
		if (intersectionObserver) return;

		intersectionObserver = new IntersectionObserver((entries) => {
			entries.forEach((entry) => {
				const eventName = entry.isIntersecting ? 'enterViewport' : 'exitViewport';
				entry.target.dispatchEvent(new CustomEvent(eventName));
			});
		}, ioConfiguration);
	}

	//@ts-ignore
	function viewport(element) {
		ensureIntersectionObserver();

		// @ts-ignore
		intersectionObserver.observe(element);

		return {
			destroy() {
				// @ts-ignore
				intersectionObserver.unobserve(element);
			}
		};
	}

	function elementCopied() {
		copyBannerOpacity.set(1);
		setTimeout(() => {
			copyBannerOpacity.set(0);
		}, 2000);
	}
</script>

<head>
	<title>Alessandro Zolli | Portfolio</title>
	<!-- Add other meta tags -->
</head>

<div
	class="border-2 border-[rgba(50,50,50,0.5)] p-4 bg-black fixed bottom-5 left-5 rounded-md"
	style="opacity: {$copyBannerOpacity}"
>
	<p>Send copied text to interesting people!</p>
</div>

<nav class="fixed top-0 left-0 right-0 p-2">
	<img src="/az-logo.svg" width="50px" alt="logo" />
</nav>
<section on:copy={elementCopied}>
	<section
		class="flex flex-col justify-center items-center my-12 h-[80vh]"
		style="opacity: {$sectionsOpacity[0]}"
	>
		<img
			class="max-w-xs rounded-full my-10 border-neutral-50 border-8"
			use:viewport
			on:enterViewport={() => sectionsOpacity.set([1, 0.3, 0.3, 0, 0.3])}
			src="https://media.licdn.com/dms/image/C4E03AQH0ZQ0Xe-J4AQ/profile-displayphoto-shrink_800_800/0/1653594699142?e=1679529600&v=beta&t=VWCg-Fgt9J9gvLP2TE6nXh-5LeYDMZh8R1ixHhCW56s"
			alt="Alessandro Zolli"
		/>
		<h1 class="text-4xl md:text-6xl font-semibold text-center">Hi, I'm Alessandro Zolli!</h1>
		<div class="flex my-4">
			<a
				target="_blank"
				rel="noreferrer"
				href="https://www.linkedin.com/in/alessandrozolli/"
				class="mr-2"><img src="/linkedin.png" width="30" alt="LinkedIn" /></a
			>
			<a target="_blank" rel="noreferrer" href="https://github.com/azolli" class="ml-2"
				><img src="/github.svg" width="30" alt="Github" /></a
			>
		</div>
	</section>
	<section class="max-w-xl mx-auto">
		<article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[1]}">
			<h1
				class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600"
				use:viewport
				on:enterViewport={() => sectionsOpacity.set([0.3, 1, 0.3, 0, 0.3])}
			>
				I'm Alessandro Zolli, a 19 years old engineering student and software developer.
			</h1>
		</article>
		<article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[2]}">
			<h1
				class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600"
				use:viewport
				on:enterViewport={() => sectionsOpacity.set([0.3, 0.3, 1, 0.3, 0.3])}
			>
				I'm based in Turin but I really like to explore new places and work remotely.
			</h1>
		</article>
		<article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[3]}">
			<h1
				class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600"
				use:viewport
				on:enterViewport={() => sectionsOpacity.set([0.3, 0.3, 0.3, 1, 0.3])}
			>
				I started programming at 10 years old and today I work with advanced languages such as Rust
				and a lot of frameworks.
			</h1>
		</article>
		<article class="my-40 flex flex-col justify-center" style="opacity: {$sectionsOpacity[4]}">
			<h1
				class="text-3xl font-semibold text-left text-transparent bg-clip-text bg-gradient-to-r from-blue-400 to-blue-600"
				use:viewport
				on:enterViewport={() => sectionsOpacity.set([0.3, 0.3, 0.3, 0.3, 1])}
			>
				In the free time I like skiing and playing guitar.
			</h1>
		</article>
	</section>
	<section>
		<h2 class="text-4xl font-bold text-center my-8">Education</h2>
		<div class="flex justify-center flex-wrap">
			<EducationCard
				school="Politecnico di Torino"
				degreeType="Engineering Bachelor Degree"
				year="0"
			/>
			<EducationCard
				school="Liceo Salesiano Valsalice"
				degreeType="Maturità Scientifica (Sc. App.) - 92/100"
				year="2022"
			/>
		</div>
	</section>
	<section class="mt-24">
		<h2
			use:viewport
			on:enterViewport={() => shuffleIcons()}
			class="text-4xl font-bold text-center my-8"
		>
			Most used technologies
		</h2>
		<div class="flex justify-center mt-20 flex-wrap">
			{#each icons as icn (icn)}
				<div animate:flip>
					<Langicon imgPath={`/${icn}`} />
				</div>
			{/each}
		</div>
	</section>
	<section class="mt-12">
		<h2 class="text-4xl font-bold text-center my-6">Some recent projects</h2>
		<div class="flex justify-center flex-wrap">
			<ProjectCard
				customer="Digisky S.r.l."
				role="Embedded Software Developer"
				img="https://picsum.photos/1920"
			/>
			<ProjectCard
				customer="ToVision By Xiaomi 2022"
				role="Full Stack Developer"
				img="/votazioni_tovision.png"
			/>
			<ProjectCard customer="Gen Z Now APS" role="Web Developer" img="https://picsum.photos/1920" />
		</div>
	</section>
</section>
