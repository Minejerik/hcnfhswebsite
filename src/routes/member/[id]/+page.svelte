<script lang="ts">
	import { page } from '$app/state';
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../../app.css';
	import { pb } from '$lib/pocketbase';
	import { Github, Globe, Twitter } from '@lucide/svelte';
	import HCpost from '$lib/HCpost.svelte';

	var userId = page.params.id;
	if (userId == undefined) {
		userId = '';
	}
	let user: any;
	let fail = false;
	let finished = false;

	onMount(async () => {
		try {
			// @ts-ignore
			user = await pb.collection('members').getOne(userId, { expand: 'posts.author' });
			console.log(user);
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
		<title>HC@NFHS | {user.name}</title>
	{:else if finished && fail}
		<title>HC@NFHS | Not Found!</title>
	{:else if !finished}
		<title>HC@NFHS | User</title>
	{/if}
</svelte:head>

<div class="flex min-h-screen justify-center bg-base-200 pt-20 pb-20">
	{#if finished && !fail}
		<div class="card min-h-75 w-[40%] min-w-[30%] bg-base-100 pb-20 shadow-xl">
			<div class="card-body">
				<div class="flex">
					<div class="avatar">
						<div class="max-w-64 min-w-32 rounded">
							<img
								src={pb.files.getURL(user, user.pfp, { thumb: '256x0' })}
								alt={`${user.name} Profile Picture`}
							/>
						</div>
					</div>
					<div class="place-self-center pl-10">
						<h1 class="font-title text-5xl lg:text-6xl xl:text-7xl 2xl:text-8xl">{user.name}</h1>
						<div class="divider"></div>
						<div class="flex gap-2">
							<div>
								{#if user.github}
									<a href={user.github} target="_blank">
										<div class="badge badge-info">
											<Github size="16" />
											Github
										</div>
									</a>
								{/if}
							</div>
							<div>
								{#if user.twitter}
									<a href={user.twitter} target="_blank">
										<div class="badge badge-info">
											<Twitter size="16" />
											Twitter/X
										</div>
									</a>
								{/if}
							</div>
							<div>
								{#if user.othersite}
									<a href={user.othersite} target="_blank">
										<div class="badge badge-info">
											<Globe size="16" />
											{user.othersite_name}
										</div>
									</a>
								{/if}
							</div>
						</div>
					</div>
				</div>
				<div class="divider">Blog Posts</div>
				<div class="flex gap-5 overflow-auto min-w-full">
					{#if user.expand.posts}
						{#each user.expand.posts as post}
							<div class="card card-side min-w-[10%] shrink-0 bg-base-300 shadow-sm">
								<figure>
									<img
										src={pb.files.getURL(post, post.images[0], { thumb: '0x200' })}
										alt="Movie"
									/>
								</figure>
								<div class="card-body">
									<h2 class="card-title">{post.title}</h2>
									{@html post.description}
									<div class="card-actions justify-end">
										<a class="btn btn-primary" href={`/blog_post/${post.id}`}>Read</a>
									</div>
								</div>
							</div>
						{/each}
					{:else}
						<div class="grid grid-cols-3 min-w-full">
							<div></div>
							<h1 class="text-xl place-self-center text-error">{`${user.name} has no blog posts.`}</h1>
						</div>
					{/if}
				</div>
				<!-- <div class="divider">Projects</div> -->
			</div>
		</div>
	{:else if finished && fail}
		<h1>User Not Found!</h1>
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
				<span>User not found!</span>
			</div>
		{/if}
	</div>
</div>
