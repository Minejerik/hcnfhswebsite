<script lang="ts">
	import { page } from '$app/state';
	import HCnav from '$lib/HCnav.svelte';
	import { onMount } from 'svelte';
	import '../../../app.css';
	import { pb } from '$lib/pocketbase';

    var postId = page.params.id
    if (postId == undefined){
        postId = ""
    }
    let post: any;
    let fail = false;
    let finished = false;


    onMount(async () => {
        try {
            // @ts-ignore
            post = await pb.collection("posts").getOne(postId)
            finished = true;
        } catch (error) {
            fail = true;
            finished = true;
        }
    })

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

<div class="bg-base-200 min-h-screen pt-15 text-center">
    
    {#if finished && !fail}
        <h1>{post.title}</h1>
    {:else if finished && fail}
        <h1>Post Not Found!</h1>
    <!-- svelte-ignore block_empty -->
    {:else if !finished}
        &nbsp;
    {/if}
</div>

<div class="content-center justify-center flex">
  <div class="fixed bottom-0 w-200 justify-center pb-5">
    {#if fail}
    <div role="alert" class="alert alert-error" id="submit_error">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 shrink-0 stroke-current" fill="none" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
      <span>Post not found!</span>
    </div>
    {/if}
  </div>
</div>