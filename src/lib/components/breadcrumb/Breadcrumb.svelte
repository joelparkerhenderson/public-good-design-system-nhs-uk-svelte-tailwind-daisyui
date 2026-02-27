<script lang="ts">
  import type { BreadcrumbProps } from '$lib/types.js';

  interface Props extends BreadcrumbProps {}

  let {
    items = [],
    labelText = 'Breadcrumb',
    collapseOnMobile = false,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const lastItem = $derived(items[items.length - 1]);

  const navAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<nav
  class="public-good-breadcrumb breadcrumbs text-sm {classes}"
  aria-label={labelText}
  {...navAttributes}
>
  <!-- Full breadcrumb for desktop -->
  <ol class="public-good-breadcrumb__list {collapseOnMobile ? 'hidden sm:flex' : ''}">
    {#each items as item}
      <li class="public-good-breadcrumb__item">
        {#if item.href}
          <a
            class="public-good-breadcrumb__link link link-hover"
            href={item.href}
            {...item.attributes || {}}
          >
            {item.text}
          </a>
        {:else}
          <span class="text-base-content/70">{item.text}</span>
        {/if}
      </li>
    {/each}
  </ol>

  <!-- Mobile back link (only shown when collapseOnMobile is true) -->
  {#if collapseOnMobile && lastItem}
    <div class="public-good-breadcrumb__back sm:hidden">
      <a
        class="public-good-breadcrumb__backlink btn btn-ghost btn-sm flex items-center gap-2"
        href={lastItem.href || '#'}
        {...lastItem.attributes || {}}
      >
        <svg
          class="w-4 h-4"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          fill="currentColor"
          aria-hidden="true"
        >
          <path d="M8.5 12c0-.3.1-.5.3-.7l5-5c.4-.4 1-.4 1.4 0s.4 1 0 1.4L10.9 12l4.3 4.3c.4.4.4 1 0 1.4s-1 .4-1.4 0l-5-5c-.2-.2-.3-.4-.3-.7z"></path>
        </svg>
        <span class="sr-only">Back to</span>
        {lastItem.text}
      </a>
    </div>
  {/if}
</nav>