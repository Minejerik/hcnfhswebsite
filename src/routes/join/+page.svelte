<script lang="ts">
	import HCnav from '$lib/HCnav.svelte';
	import { pb } from '$lib/pocketbase';
	import '../../app.css';

	let name: string;
	let email: string;

  let success = false;
  let fail = false;

	async function submit() {
    try {
      const form = await pb.collection('join_request').create({
        name: name,
        email: email
      });
      success = true;
    } catch (error) {
      fail = true;
    }
	}
</script>

<svelte:head>
  <title>HC@NFHS | Join</title>
</svelte:head>

<HCnav></HCnav>

<div class="hero min-h-screen bg-base-200">
	<div class="hero-content text-center">
		<div class="card w-200 w-max bg-base-100 shadow-2xl">
			<div class="card-body w-96">
				<h1 class="text-2xl font-bold">Join Hackclub @ NFHS</h1>
				<form on:submit={submit}>
					<fieldset class="fieldset">
						<legend class="fieldset-legend">What should we call you?</legend>
						<input
							type="text"
							class="input"
							placeholder="John Phillips"
							required
							bind:value={name}
						/>
					</fieldset>
					<fieldset class="fieldset">
						<legend class="fieldset-legend">How should we contact you?</legend>
						<input
							type="email"
							class="input"
							placeholder="example@gmail.com"
							required
							bind:value={email}
						/>
					</fieldset>
					<br />
					<button type="submit" class="btn btn-wide btn-soft btn-primary">Submit!</button>
				</form>
			</div>
		</div>
	</div>
</div>

<div class="content-center justify-center flex">
  <div class="fixed bottom-0 w-200 justify-center pb-5">
    {#if success}
    <div role="alert" class="alert alert-success" id="submit_success">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 shrink-0 stroke-current" fill="none" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
      <span>Your form submitted successfully, expect to be contacted soon!</span>
    </div>
    {/if}
    {#if fail}
    <div role="alert" class="alert alert-error" id="submit_error">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 shrink-0 stroke-current" fill="none" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
      </svg>
      <span>Something went wrong with submission! Please try again later!</span>
    </div>
    {/if}
  </div>
</div>