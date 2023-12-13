<script lang="ts">
	import { createEventDispatcher } from "svelte";
	import Fa from "svelte-fa";
	import { faBars, faEllipsisVertical } from "@fortawesome/free-solid-svg-icons";

	export let base = "/";
	export let isSidebarExpanded: boolean;
	export let sidebarWidthCollapsedPx: number;
	export let headerHeightPx: number;

	const dispatch = createEventDispatcher();

	function toggleSidebarMode() {
		dispatch("toggleSidebarMode");
	}
</script>

<header class="fixed z-30 flex w-full bg-gray-800 text-white" style="height: {headerHeightPx}px;">
	<button
		class="flex items-center justify-center"
		style="width: {sidebarWidthCollapsedPx}px;"
		on:click={toggleSidebarMode}
	>
		<Fa icon={isSidebarExpanded ? faEllipsisVertical : faBars} />
	</button>
	<ul class="flex h-full w-full">
		<li>
			<a href="{base}">
				<h1>
					<slot name="title">Dogma</slot>
				</h1>
			</a>
		</li>
		<li>
			<a href="{base}">
				<slot name="logo">
					Logo
				</slot>
			</a>
		</li>
	</ul>
</header>