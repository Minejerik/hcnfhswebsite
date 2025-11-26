<script>
	export let post;
	export let pb;
</script>

<div
	class="card h-50 w-96 min-w-50 flex-none bg-base-100 transition duration-300 ease-in-out outline-solid hover:scale-101 shadow-xl"
>
	<a href={`blog_post/${post.id}`} class="h-50 rounded-lg bg-base-100">
		<figure>
			<img src={pb.files.getURL(post, post.images[0], { thumb: '400x0' })} alt="For post" />
		</figure>
		<div class="card-body rounded-b-lg bg-base-300">
			<h2 class="card-title">{post.title}</h2>
			<p class="prose">{@html post.description}</p>
			<div class="divider mt-0 mb-1"></div>
			<div class="card-actions flex">
				<div class="avatar">
					<div class="w-7 rounded">
						<img
							src={pb.files.getURL(post.expand.author, post.expand.author.pfp, { thumb: '32x32' })}
							alt="Tailwind-CSS-Avatar-component"
						/>
					</div>
				</div>
				<span class="text-xl">{post.expand.author.name}</span>
				<span class="text-xl">{post.took_place}</span>
			</div>
		</div>
	</a>
</div>
