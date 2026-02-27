<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface ContentsListItem {
    href?: string;
    text: string;
    current?: boolean;
  }

  interface ContentsListProps extends BaseComponentProps {
    items: ContentsListItem[];
  }

  interface Props extends ContentsListProps {}

  let {
    items = [],
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const navAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<nav
  class="public-good-contents-list {classes}"
  aria-label="Pages in this guide"
  {...navAttributes}
>
  <h2 class="sr-only">Contents</h2>

  <ol class="public-good-contents-list__list menu menu-compact bg-base-200 rounded-box p-2 space-y-1">
    {#each items as item}
      <li class="public-good-contents-list__item">
        {#if item.current}
          <span
            class="public-good-contents-list__current font-medium text-primary flex items-center"
            aria-current="page"
          >
            <span class="w-2 h-2 bg-primary rounded-full mr-3"></span>
            {item.text}
          </span>
        {:else}
          <a
            class="public-good-contents-list__link hover:bg-base-300 rounded-btn px-3 py-2 flex items-center"
            href={item.href || '#'}
          >
            <span class="w-2 h-2 border border-base-content/30 rounded-full mr-3"></span>
            {item.text}
          </a>
        {/if}
      </li>
    {/each}
  </ol>
</nav>