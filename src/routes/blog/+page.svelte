<script lang="ts">
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../app.css';
	import { pb } from '$lib/pocketbase';
	import HCpost from '$lib/HCpost.svelte';

	let blogList: any[] = [];

	onMount(async () => {
		const blogListPB = await pb.collection('posts').getFullList({
			sort: '-took_place',
			expand: "author"
		});

		blogList = blogListPB;
		console.log(blogList)
	});
</script>

<HCnav></HCnav>

<svelte:head>
	<title>HC@NFHS | Blog</title>
</svelte:head>

<div class="min-h-screen bg-base-200 pt-25 pr-[2%] pl-[2%]">
	<div class="flex flex-wrap gap-4 gap-y-75">
			{#each blogList as post}
				<HCpost pb={pb} post={post}></HCpost>
			{/each}
	</div>
</div>
