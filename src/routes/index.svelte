<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import { onMount } from 'svelte';
	import { showData, perPage, offsetPage, currentTag } from '../store';

	import { initMasonry } from '$lib/utils';

	import Hero from '$lib/hero/HeroDefault.svelte';
	import CardItem from '$lib/event-item/CardItem.svelte';
	import Pagination from '$lib/pagination/Pagination.svelte';
	import Blob from '$lib/decoration/Blob.svelte';

	onMount(() => {
		currentTag.set('');
		initMasonry();
	});
</script>

<svelte:head>
	<title>Belajar daring bersama PHPID</title>

	<meta property="og:title" content="Belajar daring bersama PHPID" />
	<meta
		property="og:description"
		content="Belajar bersama melalui webinar yang diadakan oleh komunitas PHPID"
	/>

	<meta name="twitter:title" content="Belajar daring bersama PHPID" />
	<meta
		name="twitter:description"
		content="Belajar bersama melalui webinar yang diadakan oleh komunitas PHPID"
	/>
</svelte:head>

<section data-page="home">
	<Hero />
	<article class="max-w-5xl px-4 lg:px-0 mx-auto tracking-content">
		{#if $showData.length > 0}
			<Pagination className="mt-8" />
		{/if}
		{#if $showData.length > 0}
			<div
				id="content-speaker"
				class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 md:gap-x-6 gap-y-5 md:gap-y-6 mt-10 relative"
			>
				<Blob className="absolute top-32 left-0 dark:text-emerald-500 text-emerald-500/50" />
				<Blob
					className="absolute scale-x-[-1] -bottom-48 right-0 dark:text-red-500 text-red-500/50"
				/>
				{#each $showData.slice($offsetPage, $offsetPage + $perPage) as item (`${item.id}${item.slug}`)}
					<CardItem {item} />
				{/each}
			</div>
		{/if}
	</article>
	{#if $showData.length > 0}
		<Pagination className="mt-4 px-4 lg:px-0" />
	{/if}
</section>
