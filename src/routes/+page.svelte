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
		<div class="card w-200 w-max bg-base-100 shadow-2xl">
    <div class="max-w-md">
      <div class="card-body">

        <h1 class="text-5xl font-bold">Hello! 👋</h1>
        <p class="py-6 pb-0 pt-1">
          Hackclub @ NFHS is a <a href="https://hackclub.com" class="link">Hack Club</a>, dedicated to making computer science and related topics more accessable to students of North Farmington High School.
        </p>
        <div class="divider mt-0"></div>
        <a class="btn btn-primary" href="/join">Join</a>
        <a class="btn btn-secondary" href="/about">Learn more</a>
        <a class="btn btn-success" href="https://hcb.hackclub.com/donations/start/hackclub-nfhs?message=From+HC%40NFHS+Website">Donate</a>
      </div>
    </div>
    </div>
  </div>
</div>
