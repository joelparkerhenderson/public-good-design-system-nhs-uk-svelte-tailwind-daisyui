<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface InsetTextProps extends BaseComponentProps {
    text?: string;
    html?: string;
  }

  interface Props extends InsetTextProps {}

  let {
    text,
    html,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const insetTextAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<div
  class="public-good-inset-text bg-base-200 border-l-4 border-primary p-4 my-4 {classes}"
  {...insetTextAttributes}
>
  <span class="sr-only">Information: </span>

  {#if children}
    {@render children()}
  {:else if html}
    {@html html}
  {:else if text}
    <p class="m-0">{text}</p>
  {/if}
</div>