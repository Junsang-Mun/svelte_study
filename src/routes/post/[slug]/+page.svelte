<script>
	import { onMount } from "svelte";
	import { error } from "@sveltejs/kit";
	import { page } from "$app/stores";
	const apiUrl = "http://localhost:8080/api";
	let data = {title: '', content: 'Please wait, Loading...', date: ''};

	onMount(async () => {
		const result = await fetch(`${apiUrl}/posts/${$page.params.slug}`);
		const json = await result.json();
		console.log(json);
		if (json.success !== true)
			throw error(404, "Not found");
		console.log
		data = {
			title: json.data.title,
			content: json.data.body,
			date: json.data.date,
		};
	});
</script>

{#key data.content}
	<h1>{data.title}</h1>
	<p>{@html data.content}</p>
{/key}
