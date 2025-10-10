<script lang="ts">
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../app.css';
	import { pb } from '$lib/pocketbase';

	let blogList: any[] = [];

	onMount(async () => {
		const blogListPB = await pb.collection('posts').getFullList({
			sort: '-took_place'
		});

		blogList = blogListPB;
	});
</script>

<HCnav></HCnav>

<svelte:head>
	<title>HC@NFHS | Blog</title>
</svelte:head>

<div class="min-h-screen bg-base-200 pt-25 pr-15 pl-15">
	<div class="flex flex-wrap gap-4">
		<div class="bg-base-100">
			{#each blogList as post}
				<div
					class="card h-50 w-96 min-w-50 bg-base-100 transition duration-300 ease-in-out outline-solid hover:scale-101"
				>
					<a href={`blog_post/${post.id}`} class="h-50 rounded-xl bg-base-100">
						<figure>
							<img src={pb.files.getURL(post, post.images[0], { thumb: '400x0' })} alt="For post" />
						</figure>
						<div class="card-body rounded-b-xl bg-base-300">
							<h2 class="card-title">{post.title}</h2>
							<p>{@html post.description}</p>
							<hr />
							<div class="card-actions">
								<span>Written by: {post.author}</span>
								<div class="text-right">
									<span>{post.took_place}</span>
								</div>
							</div>
						</div>
					</a>
				</div>
			{/each}
		</div>
	</div>
</div>
