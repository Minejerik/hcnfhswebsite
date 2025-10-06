<script lang="ts">
	import HCnav from '$lib/HCnav.svelte';
	import { pb } from '$lib/pocketbase';
	import '../../app.css';

  let name: string;
  let email: string;

	async function submit() {
    const form = await pb.collection("join_request").create({
      "name": name,
      "email": email
    })
  }
</script>

<HCnav></HCnav>

<div class="hero min-h-screen bg-base-200">
	<div class="hero-content w-296 text-center">
		<div class="card w-200 w-max bg-base-100 shadow-2xl">
			<div class="card-body w-96">
				<h1 class="card-title">Join Hackclub @ NFHS</h1>
				<form on:submit={submit}>
					<fieldset class="fieldset">
						<legend class="fieldset-legend">What should we call you?</legend>
						<input type="text" class="input" placeholder="John Phillips" required bind:value={name}/>
					</fieldset>
					<fieldset class="fieldset">
						<legend class="fieldset-legend">How should we contact you?</legend>
						<input type="email" class="input" placeholder="example@gmail.com" required bind:value={email}/>
					</fieldset>
          <br>
          <button type="submit" class="btn btn-wide btn-soft btn-primary">Submit!</button>
				</form>
			</div>
		</div>
	</div>
</div>
