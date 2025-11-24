<script>
	export let post;
	export let pb;
</script>

<div
	class="card h-50 w-96 min-w-50 flex-none bg-base-100 transition duration-300 ease-in-out outline-solid hover:scale-101"
>
	<a href={`blog_post/${post.id}`} class="h-50 rounded-xl bg-base-100">
		<figure>
			<img src={pb.files.getURL(post, post.images[0], { thumb: '400x0' })} alt="For post" />
		</figure>
		<div class="card-body rounded-b-xl bg-base-300">
			<h2 class="card-title">{post.title}</h2>
			<p>{@html post.description}</p>
			<hr />
			<div class="card-actions">
				<span>Written by: {post.expand.author.name}</span>
				<div class="text-right">
					<span>{post.took_place}</span>
				</div>
			</div>
		</div>
	</a>
</div>
