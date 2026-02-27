<script lang="ts">
  import type { BackLinkProps } from '$lib/types.js';

  interface Props extends BackLinkProps {}

  let {
    text = 'Back',
    html,
    href = '#',
    element = 'a',
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const linkAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<div class="public-good-back-link {classes}">
  {#if element === 'button'}
    <button
      class="public-good-back-link__link btn btn-ghost btn-sm flex items-center gap-2 p-0 h-auto min-h-0"
      {...linkAttributes}
    >
      <svg
        class="public-good-icon public-good-icon__chevron-left w-6 h-6"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        aria-hidden="true"
        fill="currentColor"
      >
        <path d="M8.5 12c0-.3.1-.5.3-.7l5-5c.4-.4 1-.4 1.4 0s.4 1 0 1.4L10.9 12l4.3 4.3c.4.4.4 1 0 1.4s-1 .4-1.4 0l-5-5c-.2-.2-.3-.4-.3-.7z"></path>
      </svg>

      {#if html}
        {@html html}
      {:else}
        {text}
      {/if}
    </button>
  {:else}
    <a
      class="public-good-back-link__link btn btn-ghost btn-sm flex items-center gap-2 p-0 h-auto min-h-0 no-underline"
      {href}
      {...linkAttributes}
    >
      <svg
        class="public-good-icon public-good-icon__chevron-left w-6 h-6"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 24 24"
        aria-hidden="true"
        fill="currentColor"
      >
        <path d="M8.5 12c0-.3.1-.5.3-.7l5-5c.4-.4 1-.4 1.4 0s.4 1 0 1.4L10.9 12l4.3 4.3c.4.4.4 1 0 1.4s-1 .4-1.4 0l-5-5c-.2-.2-.3-.4-.3-.7z"></path>
      </svg>

      {#if html}
        {@html html}
      {:else}
        {text}
      {/if}
    </a>
  {/if}
</div>