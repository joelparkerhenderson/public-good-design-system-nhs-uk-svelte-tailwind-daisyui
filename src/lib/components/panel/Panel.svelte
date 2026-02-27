<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface PanelProps extends BaseComponentProps {
    titleText?: string;
    titleHtml?: string;
    text?: string;
    html?: string;
    headingLevel?: 1 | 2 | 3 | 4 | 5 | 6;
  }

  interface Props extends PanelProps {}

  let {
    titleText,
    titleHtml,
    text,
    html,
    headingLevel = 1,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const panelAttributes = $derived({
    ...attributes,
    ...restProps
  });

  const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);
</script>

<div
  class="public-good-panel bg-primary text-primary-content p-6 rounded-lg shadow-lg {classes}"
  {...panelAttributes}
>
  {#if titleText || titleHtml}
    <svelte:element this={HeadingTag} class="public-good-panel__title text-3xl font-bold mb-4">
      {#if titleHtml}
        {@html titleHtml}
      {:else}
        {titleText}
      {/if}
    </svelte:element>
  {/if}

  {#if children || html || text}
    <div class="public-good-panel__body">
      {#if children}
        {@render children()}
      {:else if html}
        {@html html}
      {:else}
        <p class="m-0">{text}</p>
      {/if}
    </div>
  {/if}
</div>