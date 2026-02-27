<script lang="ts">
  import type { WarningCalloutProps } from '$lib/types';

  interface Props extends WarningCalloutProps {}

  let {
    heading = 'Important',
    headingHtml = '',
    headingLevel = 3,
    text = '',
    html = '',
    children,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);

  const calloutAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<div
  class="public-good-warning-callout bg-yellow-50 border-l-4 border-yellow-400 p-4 my-4 {classes}"
  role="region"
  aria-label={heading}
  {...calloutAttributes}
>
  <svelte:element this={HeadingTag}
    class="public-good-warning-callout__label text-lg font-semibold mb-2 text-yellow-800"
  >
    <span>
      <span class="sr-only">Important: </span>
      {#if headingHtml}
        {@html headingHtml}
      {:else}
        {heading}
      {/if}
    </span>
  </svelte:element>

  <div class="public-good-warning-callout__content text-gray-800">
    {#if children}
      {@render children()}
    {:else if html}
      {@html html}
    {:else if text}
      <p class="mb-0">{text}</p>
    {/if}
  </div>
</div>