<script lang="ts">
	import HCnav from '$lib/HCnav.svelte';
	import logo from '$lib/assets/logos/NFHS Hack club logo.png';
	import front from '$lib/assets/leader_images/front_processed.png';
	import left from '$lib/assets/leader_images/left_processed.png';
	import right from '$lib/assets/leader_images/right_processed.png';
	import { onMount } from 'svelte';
	import '../../app.css';
	import { pb } from '$lib/pocketbase';

	let userList: any[] = [];

	onMount(async () => {
		const userListPB = await pb.collection('members').getFullList({
			sort: 'name'
		});

		userList = userListPB;
		console.log(userList);
	});
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
			<div class="card-body flex">
				<div class="card-title flex justify-center">
					<h2>About Hackclub @ NFHS!</h2>
				</div>
				<div class="prose prose-lg max-w-none">
					Hackclub @ NFHS is dedicated to making computer science and programming more accessable to
					those at North Farmington High School. <br />
					We meet semi-regularly after-school Wednesdays in room 400.
				</div>
				<div class="card-actions justify-self-end">
					<a
						href="https://hcb.hackclub.com/donations/start/hackclub-nfhs?message=From+HC%40NFHS+Website"
						class="btn btn-xs btn-primary sm:btn-sm md:btn-md">Support HC@NFHS by donating!</a
					>
					<a
						href="https://dashboard.hackclub.com/join-club?code=XUNLDNL5"
						class="btn btn-xs btn-secondary sm:btn-sm md:btn-md"
						>Join the HC@NFHS Hack Club Dashboard!</a
					>
				</div>
			</div>
		</div>

		<div class="card mt-10 min-h-80 min-w-[50%] bg-base-100 shadow-xl">
			<div class="card-body">
				<div class="card-title flex justify-center">
					<h2>Hackclub @ NFHS Members!</h2>
				</div>
				<div class="flex gap-5 flex-wrap">
					{#if userList.length > 0}
						{#each userList as user}
							<a class="hover-3d" href={`/member/${user.id}`}>
								<div class="card max-w-45 bg-base-300 shadow-lg">
									<figure>
										<img
											src={pb.files.getURL(user, user.pfp, { thumb: '256x0' })}
											alt={`${user.name} Profile Picture`}
										/>
									</figure>
									<div class="card-body">
										<h1 class="card-title justify-center">{user.name}</h1>
									</div>
								</div>
								<!-- 8 empty divs needed for the 3D effect -->
								<div></div>
								<div></div>
								<div></div>
								<div></div>
								<div></div>
								<div></div>
								<div></div>
								<div></div>
							</a>
						{/each}
					{:else}
					{#each { length: 6 } as _}
						<div class="card max-w-45 bg-base-200 shadow-lg">
							<figure>
								<div class="h-45 w-45 skeleton"></div>
							</figure>
							<div class="card-body">
								<div class="h-4 w-20 skeleton"></div>
							</div>
						</div>
					{/each}
					{/if}
				</div>
			</div>
		</div>
		
		<div class="card mt-10 card-side min-h-75 min-w-[50%] bg-base-100 shadow-xl">
			<figure class="hover-gallery max-w-60">
				<!-- TODO: replace photos w my own -->
				<img src={front} alt="the hc@nfhs leader" />
				<img src={left} alt="the hc@nfhs leader" />
				<img src={front} alt="the hc@nfhs leader" />
				<img src={right} alt="the hc@nfhs leader" />
			</figure>
			<div class="card-body">
				<div class="card-title flex justify-center">
					<h2>About the HC@NFHS Leader!</h2>
				</div>
				<div>
					<p class="prose prose-xl max-w-none">
						<b>Hello!</b> <br />
						I'm Jaan-Erik, the leader of HC@NFHS. I started this club because I wanted to spread computer
						science and programming to more people!
					</p>
				</div>
			</div>
		</div>
	</div>
</div>
