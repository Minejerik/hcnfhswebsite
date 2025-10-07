<script lang="ts">
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../app.css';
	import { pb } from '$lib/pocketbase';

    let blogList: any[] = [];

    onMount(async () => {
        const blogListPB = await pb.collection("posts").getFullList({
            sort: "-took_place"
        })

        blogList = blogListPB
    })
</script>

<HCnav></HCnav>

<svelte:head>
	<title>HC@NFHS | Blog</title>
</svelte:head>

<div class="min-h-screen bg-base-200 pt-25 pl-15 pr-15">
    {#each blogList as post}
	<div class="flex flex-wrap gap-4">
		<div class="bg-base-100">
			<div class="card h-50 w-96 min-w-50 bg-base-100 shadow-sm outline-solid">
				<a href={`blog_post/${post.id}`} class="h-50 bg-base-100">
					<figure>
						<img
							src={pb.files.getURL(post, post.images[0], {thumb: "400x0"})}
							alt="For post"
						/>
					</figure>
					<div class="card-body bg-base-300">
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
		</div>
	</div>
    {/each}
</div>
