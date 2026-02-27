<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface SkipLinkProps extends BaseComponentProps {
    href?: string;
    text?: string;
    html?: string;
  }

  interface Props extends SkipLinkProps {}

  let {
    href = '#maincontent',
    text = 'Skip to main content',
    html,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const skipLinkAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<a
  class="public-good-skip-link btn btn-primary btn-sm {classes}"
  {href}
  {...skipLinkAttributes}
>
  {#if children}
    {@render children()}
  {:else if html}
    {@html html}
  {:else}
    {text}
  {/if}
</a>

<style>
  .public-good-skip-link {
    position: fixed;
    top: 8px;
    left: 8px;
    z-index: 9999;
    opacity: 0;
    transform: translateY(-100%);
    transition: opacity 0.2s, transform 0.2s;
  }

  .public-good-skip-link:focus {
    opacity: 1;
    transform: translateY(0);
    outline: 2px solid currentColor;
    outline-offset: 2px;
  }
</style>