<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface HintProps extends BaseComponentProps {
    text?: string;
    html?: string;
    id?: string;
  }

  interface Props extends HintProps {}

  let {
    text,
    html,
    id,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const hintAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(id ? { id } : {})
  });
</script>

<div
  class="public-good-hint text-sm text-base-content/70 {classes}"
  {...hintAttributes}
>
  {#if children}
    {@render children()}
  {:else if html}
    {@html html}
  {:else}
    {text}
  {/if}
</div>