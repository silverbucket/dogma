<script lang="ts">
	import Fa from "svelte-fa";
	import type { IconDefinition } from "@fortawesome/free-solid-svg-icons";
	import { page } from "$app/stores";

	export let url: string;
	export let label: string;
	export let icon: IconDefinition;
	export let external = false;
	export let recursive = false;
	export let disabled = false;
	export let disabledMessage = "";
	export let additionalActiveUrls: string[] = [];
	export let sidebarWidthCollapsedPx: number;
	export let sidebarWidthsDifferencePx: number;

	let isHoveredOver = false;

	let id = "";

	function show() {
		isHoveredOver = true;
	}

	function hide() {
		isHoveredOver = false;
	}

	$: bgClass = isHoveredOver ? "bg-cyan-500" : isActive ? "bg-cyan-800" : "bg-cyan-500";
	$: colorClass = isActive && !isHoveredOver ? "text-blue-4" : "";
	$: colorClassForDisabled = disabled ? "text-grey-1" : "";
	$: title = disabled ? disabledMessage : "";

	let pathname: string;
	$: pathname = $page.url.pathname;

	let isActive = checkWhetherIsActive();

	function checkWhetherIsActive(): boolean {
		if (!pathname) return false;
		if (recursive) {
			if (pathname.startsWith(url)) return true;
		} else {
			if (pathname === url) return true;
		}
		if (!additionalActiveUrls) return false;
		return additionalActiveUrls.some((url) => pathname.startsWith(url));
	}
</script>

<li {title} data-test-id={"menu-item:" + id} class="h-12">
	<a
		class:pointer-events-none={disabled}
		class="relative block h-full"
		href={url}
		target={external ? "_blank" : undefined}
		on:mouseenter={show}
		on:mouseleave={hide}
	>
		<div
			class="absolute right-0 flex h-full items-center {bgClass} {colorClassForDisabled}"
			style="width: {sidebarWidthsDifferencePx}px; left: {isHoveredOver
                ? `${sidebarWidthCollapsedPx}px`
                : ''};"
		>
			{label}
		</div>
		<div
			class="absolute flex h-full items-center justify-center {bgClass} {colorClass} {colorClassForDisabled}"
			style="width: {sidebarWidthCollapsedPx}px;"
		>
			<Fa {icon} />
		</div>
	</a>
</li>
