<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface ErrorMessageProps extends BaseComponentProps {
    id?: string;
    text?: string;
    html?: string;
    visuallyHiddenText?: string;
  }

  interface Props extends ErrorMessageProps {}

  let {
    id,
    text,
    html,
    visuallyHiddenText = 'Error',
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const spanAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<span
  class="public-good-error-message text-error font-medium text-sm {classes}"
  {id}
  {...spanAttributes}
>
  {#if visuallyHiddenText}
    <span class="sr-only">{visuallyHiddenText}:</span>{' '}
  {/if}
  {#if html}
    {@html html}
  {:else}
    {text}
  {/if}
</span>