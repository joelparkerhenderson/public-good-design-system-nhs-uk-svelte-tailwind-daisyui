<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface PaginationProps extends BaseComponentProps {
    previousUrl?: string;
    previousPage?: string;
    nextUrl?: string;
    nextPage?: string;
  }

  interface Props extends PaginationProps {}

  let {
    previousUrl,
    previousPage,
    nextUrl,
    nextPage,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const paginationAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<nav
  class="public-good-pagination {classes}"
  aria-label="Pagination"
  {...paginationAttributes}
>
  <ul class="flex justify-between items-center space-x-4">
    {#if previousUrl && previousPage}
      <li class="public-good-pagination-item--previous">
        <a
          class="public-good-pagination__link btn btn-outline flex items-center gap-2 px-4 py-2"
          href={previousUrl}
        >
          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M4.1 12.3l2.7 3c.2.2.5.2.7 0 .1-.1.1-.2.1-.3v-2h11c.6 0 1-.4 1-1s-.4-1-1-1h-11V9c0-.2-.1-.4-.3-.5h-.2c-.1 0-.3.1-.4.2l-2.7 3c0 .2 0 .4.1.6z"></path>
          </svg>

          <div class="text-left">
            <span class="public-good-pagination__title block text-sm">Previous</span>
            <span class="sr-only">:</span>
            <span class="public-good-pagination__page block font-semibold">{previousPage}</span>
          </div>
        </a>
      </li>
    {:else}
      <li></li>
    {/if}

    {#if nextUrl && nextPage}
      <li class="public-good-pagination-item--next">
        <a
          class="public-good-pagination__link btn btn-outline flex items-center gap-2 px-4 py-2"
          href={nextUrl}
        >
          <div class="text-right">
            <span class="public-good-pagination__title block text-sm">Next</span>
            <span class="sr-only">:</span>
            <span class="public-good-pagination__page block font-semibold">{nextPage}</span>
          </div>

          <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M19.6 11.66l-2.73-3A.51.51 0 0 0 16 9v2H5a1 1 0 0 0 0 2h11v2a.5.5 0 0 0 .32.46.39.39 0 0 0 .18 0 .52.52 0 0 0 .37-.16l2.73-3a.5.5 0 0 0 0-.64z"></path>
          </svg>
        </a>
      </li>
    {:else}
      <li></li>
    {/if}
  </ul>

  {#if children}
    {@render children()}
  {/if}
</nav>