<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface DoDontListItem {
    item: string;
  }

  interface DoDontListProps extends BaseComponentProps {
    title: string;
    type: 'tick' | 'cross';
    items: DoDontListItem[];
    headingLevel?: 1 | 2 | 3 | 4 | 5 | 6;
    hidePrefix?: boolean;
  }

  interface Props extends DoDontListProps {}

  let {
    title,
    type = 'tick',
    items = [],
    headingLevel = 3,
    hidePrefix = false,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const listClasses = $derived(
    `public-good-do-dont-list__list space-y-3 ${type === 'tick' ? 'text-success' : 'text-error'}`
  );

  const iconClasses = $derived(
    `w-6 h-6 ${type === 'tick' ? 'text-success' : 'text-error'} flex-shrink-0 mt-0.5`
  );

  const containerAttributes = $derived({
    ...attributes,
    ...restProps
  });

  const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);
</script>

<div class="public-good-do-dont-list {classes}" {...containerAttributes}>
  <svelte:element this={HeadingTag} class="public-good-do-dont-list__label text-lg font-semibold mb-4">
    {title}
  </svelte:element>

  <ul class={listClasses} role="list">
    {#each items as item}
      <li class="flex gap-3 items-start">
        {#if type === 'cross'}
          <svg
            class={iconClasses}
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            aria-hidden="true"
            fill="currentColor"
          >
            <path d="M17 18.5c-.4 0-.8-.1-1.1-.4l-10-10c-.6-.6-.6-1.6 0-2.1.6-.6 1.5-.6 2.1 0l10 10c.6.6.6 1.5 0 2.1-.3.3-.6.4-1 .4z"></path>
            <path d="M7 18.5c-.4 0-.8-.1-1.1-.4-.6-.6-.6-1.5 0-2.1l10-10c.6-.6 1.5-.6 2.1 0 .6.6.6 1.5 0 2.1l-10 10c-.3.3-.6.4-1 .4z"></path>
          </svg>
        {:else}
          <svg
            class={iconClasses}
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="none"
            aria-hidden="true"
            stroke="currentColor"
          >
            <path stroke-width="4" stroke-linecap="round" d="M18.4 7.8l-8.5 8.4L5.6 12"></path>
          </svg>
        {/if}

        <span class="text-base-content">
          {#if type === 'cross' && !hidePrefix}do not {/if}{item.item}
        </span>
      </li>
    {/each}
  </ul>
</div>