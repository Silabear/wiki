<script lang="ts">
  import { windowInfo } from "$lib/stores.svelte";
  import type { Snippet } from "svelte";
  import IconExpand from "~icons/tabler/chevron-right";

  type Props = {
    name: string;
    icon: any;
    children: Snippet;
  };

  const { children, name, icon }: Props = $props();

  const Icon = $derived(icon);
</script>

<details ontoggle={() => (windowInfo.isNavOpen = true)} class="w-full group marker:hidden">
  <summary
    class="rounded-lg cursor-pointer p-1 w-full flex gap-2 items-center text-left hover:bg-stone-700 hover:text-white hover:font-medium marker:hidden">
    <Icon />
    {#if windowInfo.isNavOpen}
      <span class="grow">{name}</span>
      <IconExpand class="motion-safe:transition-all group-open:rotate-90 rotate-0" />
    {/if}
  </summary>
  {#if windowInfo.isNavOpen}
    <div class="flex flex-col ml-4 pb-2">
      {@render children()}
    </div>
  {/if}
</details>
