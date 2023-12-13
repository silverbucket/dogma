<script>
	import "../app.css";
	import { base } from "$app/paths";
	import Header from "$components/framework/Header.svelte";
	import Footer from "$components/framework/Footer.svelte";
	import Sidebar from '$components/framework/Sidebar.svelte';
	import { faDiagramProject } from '@fortawesome/free-solid-svg-icons';
	import SidebarItem from '$components/framework/SidebarItem.svelte';

	const headerHeightPx = 52;
	let isSidebarExpanded = false;
	const sidebarWidthCollapsedPx = 56;
	const sidebarWidthExpandedPx = 166;
	$: sidebarWidthsDifferencePx = sidebarWidthExpandedPx - sidebarWidthCollapsedPx;

	function toggleSidebarMode() {
		isSidebarExpanded = !isSidebarExpanded;
	}
</script>

<Header
	{base}
	{headerHeightPx}
	{sidebarWidthCollapsedPx}
	{isSidebarExpanded}
	on:toggleSidebarMode={toggleSidebarMode}
	>
</Header>
<div class="flex min-h-screen">

	<Sidebar
		{isSidebarExpanded}
		{headerHeightPx}
		{sidebarWidthCollapsedPx}
		{sidebarWidthExpandedPx}
	>
		<SidebarItem
			icon={faDiagramProject}
			label="Rollouts"
			url="{base}/rollouts"
			additionalActiveUrls={[`${base}/rollout/`]}
			{sidebarWidthCollapsedPx}
			{sidebarWidthsDifferencePx}
		/>

	</Sidebar>

	<div class="flex flex-1 flex-col overflow-hidden bg-blue-300" style="padding-top: {headerHeightPx}px; padding-left: {sidebarWidthCollapsedPx}px;">
		<main class="flex-1 p-4" id="page-content">
			<slot />
		</main>

		<Footer></Footer>
	</div>
</div>
