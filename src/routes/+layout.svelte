<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar } from '@skeletonlabs/skeleton';
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<a
					class="font-bold text-xl uppercase"
					href="/"
					rel="noreferrer"
				>
					Tissue Inc</a>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<a
					class="btn btn-sm variant-ghost-surface"
					href="/credits"
					rel="noreferrer"
				>
					Credits
				</a>
				<a
					class="btn btn-sm variant-ghost-surface"
					href="https://github.com/Fraser-Chapman/trak-zak"
					target="_blank"
					rel="noreferrer"
				>
					GitHub
				</a>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>
