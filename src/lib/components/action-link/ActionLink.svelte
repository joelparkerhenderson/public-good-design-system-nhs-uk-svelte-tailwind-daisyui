<script lang="ts">
  import type { ActionLinkProps } from '$lib/types.js';

  interface Props extends ActionLinkProps {}

  let {
    text,
    html,
    href,
    openInNewWindow = false,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const linkAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(openInNewWindow ? { target: '_blank', rel: 'noopener noreferrer' } : {})
  });
</script>

<div class="public-good-action-link">
  <a
    class="public-good-action-link__link btn btn-outline btn-primary flex items-center gap-2 {classes}"
    {href}
    {...linkAttributes}
  >
    <svg
      class="public-good-icon public-good-icon__arrow-right-circle w-6 h-6"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 24 24"
      aria-hidden="true"
      fill="currentColor"
    >
      <path d="M0 0h24v24H0z" fill="none"></path>
      <path d="M12 2a10 10 0 0 0-9.95 9h11.64L9.74 7.05a1 1 0 0 1 1.41-1.41l5.66 5.65a1 1 0 0 1 0 1.42l-5.66 5.65a1 1 0 0 1-1.41 0 1 1 0 0 1 0-1.41L13.69 13H2.05A10 10 0 1 0 12 2z"></path>
    </svg>

    <span class="public-good-action-link__text">
      {#if html}
        {@html html}
      {:else}
        {text}
      {/if}
    </span>
  </a>
</div>