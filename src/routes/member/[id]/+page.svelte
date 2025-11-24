<script lang="ts">
	import { page } from '$app/state';
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../../app.css';
	import { pb } from '$lib/pocketbase';

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
			user = await pb.collection('members').getOne(userId);
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
		<div class="card min-h-75 min-w-[50%] bg-base-100 pb-20 shadow-xl">
			<div class="card-body">
				<div class="flex">
					<div class="avatar">
						<div class="min-w-32 max-w-64 rounded">
							<img
							src={pb.files.getURL(user, user.pfp, { thumb: '256x0' })}
							alt={`${user.name} Profile Picture`}
							/>
						</div>
					</div>
					<div class="pl-10 place-self-center">
						<h1 class="font-title text-8xl">{user.name}</h1>
						
					</div>
				</div>
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
