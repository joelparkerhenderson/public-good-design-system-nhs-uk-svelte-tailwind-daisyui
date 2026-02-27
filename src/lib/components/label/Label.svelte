<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface LabelProps extends BaseComponentProps {
    text?: string;
    html?: string;
    for?: string;
    isPageHeading?: boolean;
  }

  interface Props extends LabelProps {}

  let {
    text,
    html,
    for: htmlFor,
    isPageHeading = false,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const labelAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(htmlFor ? { for: htmlFor } : {})
  });
</script>

{#if text || html || children}
  {#if isPageHeading}
    <h1 class="public-good-label-wrapper">
      <label
        class="public-good-label label text-3xl font-bold {classes}"
        {...labelAttributes}
      >
        {#if children}
          {@render children()}
        {:else if html}
          {@html html}
        {:else}
          {text}
        {/if}
      </label>
    </h1>
  {:else}
    <label
      class="public-good-label label {classes}"
      {...labelAttributes}
    >
      <span class="label-text">
        {#if children}
          {@render children()}
        {:else if html}
          {@html html}
        {:else}
          {text}
        {/if}
      </span>
    </label>
  {/if}
{/if}