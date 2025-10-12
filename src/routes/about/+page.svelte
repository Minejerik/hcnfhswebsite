<script>
	import HCnav from '$lib/HCnav.svelte';
	import logo from '$lib/assets/logos/NFHS Hack club logo.png';
	import front from "$lib/assets/leader_images/front_processed.png";
	import left from "$lib/assets/leader_images/left_processed.png";
	import right from "$lib/assets/leader_images/right_processed.png";
	import '../../app.css';
</script>

<svelte:head>
	<title>HC@NFHS | About</title>
</svelte:head>

<HCnav></HCnav>

<div class="flex min-h-screen justify-center bg-base-200 pt-25">
	<div class="max-w-[50%]">
		<div class="card card-side min-h-75 min-w-[50%] bg-base-100 shadow-xl">
			<figure class="max-w-60">
				<img src={logo} alt="HC @ NFHS Logo" />
			</figure>
			<div class="card-body">
				<div class="card-title flex justify-center">
					<h2>About Hackclub @ NFHS!</h2>
				</div>
				<div>
					Hackclub @ NFHS is dedicated to making computer science and programming more accessable to
					those at North Farmington High School. <br />
					We meet semi-regularly after-school Wednesdays in room 400.
				</div>
				<div class="card-actions">
					<a
						href="https://hcb.hackclub.com/donations/start/hackclub-nfhs?message=From+HC%40NFHS+Website"
						class="btn btn-primary btn-xs sm:btn-sm md:btn-md ">Support HC@NFHS by donating!</a
					>
					<a href="https://dashboard.hackclub.com/join-club?code=XUNLDNL5" class="btn btn-secondary btn-xs sm:btn-sm md:btn-md"
						>Join the HC@NFHS Hack Club Dashboard!</a
					>
				</div>
			</div>
		</div>

		<div class="card mt-10 card-side min-h-75 min-w-[50%] bg-base-100 shadow-xl">
			<figure class="hover-gallery max-w-60">
				<!-- TODO: replace photos w my own -->
				<img src={front} />
				<img src={left} />
				<img src={front} />
				<img src={right} />
			</figure>
			<div class="card-body">
				<div class="card-title flex justify-center">
					<h2>About the HC@NFHS Leader!</h2>
				</div>
				<div>
					<p class="text-lg">
						<b>Hello!</b> <br />
						I'm Jaan-Erik, the leader of HC@NFHS. I started this club because I wanted to spread computer
						science and programming to more people!
					</p>
				</div>
			</div>
		</div>
	</div>
</div>
