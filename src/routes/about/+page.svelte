<script>
	import HCnav from '$lib/HCnav.svelte';
	import '../../app.css';
</script>

<svelte:head>
	<title>HC@NFHS | About</title>
</svelte:head>

<HCnav></HCnav>

<div class="flex min-h-screen justify-center bg-base-200 pt-25">
	<div class="max-w-[50%]">
		<div class="card card-side max-h-75 min-w-[50%] bg-base-100 shadow-2xl">
			<figure class="max-w-60">
				<img src="src/lib/assets/logos/NFHS Hack club logo.png" alt="HC @ NFHS Logo" />
			</figure>
			<div class="card-body">
				<div class="card-title flex justify-center">
					<h2>About Hackclub @ NFHS!</h2>
				</div>
				<div>
            Hackclub @ NFHS is dedicated to making computer science and programming more accessable to those at North Farmington High School. <br>
            We meet semi-regularly after-school Wednesdays in room 400.
        </div>
        <div class="card-actions">
            <a href="https://dashboard.hackclub.com/join-club?code=XUNLDNL5" class="btn btn-primary">Join the HC@NFHS Hack Club Dashboard!</a>
        </div>
			</div>
		</div>

		<div class="card mt-10 card-side max-h-75 min-w-[50%] bg-base-100 shadow-2xl">
			<figure class="hover-gallery max-w-60">
				<!-- TODO: replace photos w my own -->
				<img src="https://img.daisyui.com/images/stock/daisyui-hat-1.webp" />
				<img src="https://img.daisyui.com/images/stock/daisyui-hat-2.webp" />
				<img src="https://img.daisyui.com/images/stock/daisyui-hat-3.webp" />
				<img src="https://img.daisyui.com/images/stock/daisyui-hat-4.webp" />
			</figure>
			<div class="card-body">
				<div class="card-title flex justify-center">
					<h2>About the HC@NFHS Leader!</h2>
				</div>
				<div>
					<p class="text-lg">
						<b>Hello!</b> <br> 
            I'm Jaan-Erik, the leader of HC@NFHS. I started this club because I wanted to spread computer science and programming to more people!
					</p>
				</div>
			</div>
		</div>
	</div>
</div>
