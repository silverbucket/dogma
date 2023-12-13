<script lang="ts">
	export let isSidebarExpanded: boolean;
	export let headerHeightPx: number;
	export let sidebarWidthCollapsedPx: number;
	export let sidebarWidthExpandedPx: number;
</script>

<aside
	class="fixed transition-all duration-100 z-0"
	style="min-width: {isSidebarExpanded ? sidebarWidthExpandedPx : sidebarWidthCollapsedPx}px; padding-top: {headerHeightPx}px;"
>
	<nav
		class="sticky z-30"
		style="top: 0px; height: 100vh;"
	>
		<ul class="absolute flex h-full w-full flex-col bg-gray-800 pt-3 text-white">
			<slot />
		</ul>
	</nav>
</aside>
