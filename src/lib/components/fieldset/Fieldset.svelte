<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface FieldsetLegend {
    text?: string;
    html?: string;
    classes?: string;
    isPageHeading?: boolean;
  }

  interface FieldsetProps extends BaseComponentProps {
    legend?: FieldsetLegend;
    describedBy?: string;
  }

  interface Props extends FieldsetProps {}

  let {
    legend,
    describedBy,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const fieldsetAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(describedBy ? { 'aria-describedby': describedBy } : {})
  });
</script>

<fieldset
  class="public-good-fieldset {classes}"
  {...fieldsetAttributes}
>
  {#if legend?.html || legend?.text}
    <legend class="public-good-fieldset__legend text-lg font-semibold mb-4 {legend.classes || ''}">
      {#if legend.isPageHeading}
        <h1 class="public-good-fieldset__heading text-3xl font-bold">
          {#if legend.html}
            {@html legend.html}
          {:else}
            {legend.text}
          {/if}
        </h1>
      {:else}
        {#if legend.html}
          {@html legend.html}
        {:else}
          {legend.text}
        {/if}
      {/if}
    </legend>
  {/if}

  {#if children}
    {@render children()}
  {/if}
</fieldset>