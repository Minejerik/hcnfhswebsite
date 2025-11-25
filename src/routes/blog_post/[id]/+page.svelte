<script lang="ts">
	import { page } from '$app/state';
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../../app.css';
	import { pb } from '$lib/pocketbase';

	var postId = page.params.id;
	if (postId == undefined) {
		postId = '';
	}
	let post: any;
	let fail = false;
	let finished = false;

	onMount(async () => {
		try {
			// @ts-ignore
			post = await pb.collection('posts').getOne(postId, { expand: 'author' });
			finished = true;
		} catch (error) {
			fail = true;
			finished = true;
		}
	});
</script>

<HCnav></HCnav>

<svelte:head>
	{#if finished && !fail}
		<title>HC@NFHS | {post.title}</title>
	{:else if finished && fail}
		<title>HC@NFHS | Not Found!</title>
	{:else if !finished}
		<title>HC@NFHS | Blog Post</title>
	{/if}
</svelte:head>

<div class="flex min-h-screen justify-center bg-base-200 pt-20">
	{#if finished && !fail}
		<div class="max-w-[50%]">
			<h1 class="font-title text-5xl">{post.title}</h1>
			<div class="pt-2 pb-2 flex">
				<a href={`/member/${post.author}`}>
					<h1 class="text-xl">
						<div class="avatar">
							<div class="w-8 rounded">
								<img
									src={pb.files.getURL(post.expand.author, post.expand.author.pfp, { thumb: '32x32' })}
									alt="Tailwind-CSS-Avatar-component"
								/>
							</div>
						</div>
						{post.expand.author.name}
					</h1>
				</a>
				<h2 class="text-xl">&nbsp; {post.took_place}</h2>
			</div>
			<div class="pt-5">
				<div class="carousel h-[25%] max-h-[25%]">
					<!-- TODO: Use a better solution for images -->
					{#each post.images as image}
						<div id="item1" class="carousel-item h-[25%] max-h-[25%] w-full">
							<img
								src={pb.files.getURL(post, image, { thumb: '600x0' })}
								alt={`From ${post.title}`}
								class="rounded-sm"
							/>
						</div>
					{/each}
				</div>
				<div class="divider"></div>
				<div class="prose">{@html post.body_text}</div>
			</div>
		</div>
	{:else if finished && fail}
		<h1>Post Not Found!</h1>
	{:else if !finished}
		&nbsp;
	{/if}
</div>

<div class="flex content-center justify-center">
	<div class="fixed bottom-0 w-200 justify-center pb-5">
		{#if fail}
			<div role="alert" class="alert alert-error" id="submit_error">
				<svg
					xmlns="http://www.w3.org/2000/svg"
					class="h-6 w-6 shrink-0 stroke-current"
					fill="none"
					viewBox="0 0 24 24"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
					/>
				</svg>
				<span>Post not found!</span>
			</div>
		{/if}
	</div>
</div>
