<script lang="ts">
	import { enhance } from "$app/forms";
	import { faWarning } from "@fortawesome/free-solid-svg-icons";
	import Fa from "svelte-fa";
	import type { ActionData } from "./$types";
	import debug from "debug";
	import { getSessionStore } from "$lib/stores/session";

	const log = debug("app:routes:signup:page.svelte");

	const session = getSessionStore();

	export let form: ActionData;
</script>

<section class="max-w-sm mx-auto">
	<div class="prose">
		<h1>Sign Up</h1>
	</div>

	<form class="flex flex-col gap-6 my-6" method="POST" use:enhance>
		{#if form?.error}
			<div class="alert alert-error">
				<div>
					<Fa icon={faWarning} />
					{form.error}
				</div>
			</div>
		{/if}
		<p>
			<input
				type="email"
				name="email"
				placeholder="Email..."
				class="input input-bordered w-full"
				required
				value={form?.email ?? ""}
			/>
		</p>
		<p>
			<input
				type="password"
				name="password"
				placeholder="Password..."
				class="input input-bordered w-full"
				required
			/>
		</p>
		<p>
			<input
				type="password"
				name="password-confirm"
				placeholder="Confirm password..."
				class="input input-bordered w-full"
				required
			/>
		</p>
		<p class="flex items-center gap-6 mt-6">
			<button class="btn btn-primary">Sign Up</button>
			or
			<a href="/login" class="link">Log In</a>
		</p>
	</form>

	{#if form}
		<section class="my-8">
			<h3>Form data:</h3>
			<pre>{JSON.stringify(form, null, 2)}</pre>
		</section>
	{/if}
</section>
