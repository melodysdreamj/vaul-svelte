<script lang="ts">
	import DirectionDrawer from "../(components)/direction-drawer.svelte";
	import NestedDrawer from "./nested-drawer.svelte";
	import NonDraggableDrawer from "./non-draggable-drawer.svelte";
	import ScrollableDrawer from "./scrollable-drawer.svelte";
	import SnapPointDrawer from "./snap-point-drawer.svelte";
	import { Drawer } from "../../lib/vaul/index.js";

	const directions = ["top", "left", "bottom", "right"] as const;
	let openWithScrollableContent = false;
</script>

<div class="mx-auto max-w-2xl pt-64 text-center">
	<div class="relative flex flex-col items-center justify-evenly p-8">
		<h1 class="relative mb-4 text-2xl font-semibold">Usage Examples</h1>
		<div class="mb-4">
			<NestedDrawer />
		</div>
		<div class="mb-4">
			<ScrollableDrawer />
		</div>
		<div class="mb-4">
			<SnapPointDrawer />
		</div>
		{#each directions as direction}
			<div class="mb-4">
				<DirectionDrawer {direction} />
			</div>
		{/each}
		<div class="mb-4">
			<NonDraggableDrawer />
		</div>
		<div class="mb-4">
			<Drawer.Root
				bind:open={openWithScrollableContent}
				snapPoints={[0.1, 0.9]}
				closeOnOutsideClick={false}
			>
				<Drawer.Trigger class="rounded-md bg-black px-4 py-2 text-white">
					Open Drawer (Scrollable & Background Interaction)
				</Drawer.Trigger>
				<Drawer.Portal>
					<Drawer.Overlay class="fixed inset-0 z-50 bg-black/10" style="pointer-events: none;" />
					<Drawer.Content
						class="fixed inset-x-0 bottom-0 z-50 mt-24 flex h-full max-h-[95%] flex-col rounded-t-lg border bg-background focus:outline-none"
					>
						<div class="mx-auto mb-8 h-1.5 w-12 flex-shrink-0 rounded-full bg-muted" />
						<div class="flex-1 overflow-y-auto p-4">
							<Drawer.Title class="mb-2 text-lg font-medium">
								Scrollable Content Inside Drawer
							</Drawer.Title>
							{#each Array(50) as _, i}
								<p class="py-2">Item {i + 1}</p>
							{/each}
						</div>
					</Drawer.Content>
				</Drawer.Portal>
			</Drawer.Root>
		</div>
	</div>
	<div class="mt-8 h-[1000px] bg-gray-100 p-4">
		<h2 class="text-xl font-semibold">Background Content</h2>
		<p class="mt-4">
			This is some content behind the drawer. You should be able to scroll this area even when the
			drawer is open.
		</p>
		{#each Array(50) as _, i}
			<p class="py-2">Background Item {i + 1}</p>
		{/each}
	</div>
</div>
