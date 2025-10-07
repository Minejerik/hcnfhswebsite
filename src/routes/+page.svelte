<script>
	import HCnav from '$lib/HCnav.svelte';
	import '../app.css';
</script>

<HCnav></HCnav>

<svelte:head>
  <title>HC@NFHS</title>
</svelte:head>

<div class="hero bg-base-200 min-h-screen">
  <div class="hero-content text-center">
    <div class="max-w-md">
      <h1 class="text-5xl font-bold">Hello! 👋</h1>
      <p class="py-6">
        Hackclub @ NFHS is a <a href="https://hackclub.com" class="link">Hack Club</a>, dedicated to making computer science and related topics more accessable to students of North Farmington High School.
      </p>
      <a class="btn btn-primary" href="/about">Learn more</a>
    </div>
  </div>
</div>
