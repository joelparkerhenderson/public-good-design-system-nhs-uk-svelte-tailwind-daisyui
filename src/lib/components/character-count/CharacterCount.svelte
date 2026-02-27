<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface CharacterCountProps extends BaseComponentProps {
    id?: string;
    name: string;
    label: {
      text?: string;
      html?: string;
      classes?: string;
      isPageHeading?: boolean;
    };
    value?: string;
    maxlength?: number;
    maxwords?: number;
    threshold?: number;
    rows?: number;
    spellcheck?: boolean;
    hint?: { text: string };
    errorMessage?: { text: string };
    countMessage?: { classes?: string };
    formGroup?: {
      classes?: string;
      attributes?: Record<string, string>;
    };
  }

  interface Props extends CharacterCountProps {}

  let {
    id,
    name,
    label,
    value = $bindable(''),
    maxlength,
    maxwords,
    threshold = 75,
    rows = 5,
    spellcheck = true,
    hint,
    errorMessage,
    countMessage,
    formGroup,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const elementId = $derived(id || name);
  const countId = $derived(`${elementId}-info`);

  const currentCount = $derived(
    maxwords
      ? value.trim().split(/\s+/).filter(word => word.length > 0).length
      : value.length
  );

  const remainingCount = $derived((maxlength || maxwords || 0) - currentCount);
  const isOverLimit = $derived(remainingCount < 0);

  const showWarning = $derived((() => {
    const limit = maxlength || maxwords || 0;
    const thresholdCount = Math.floor((threshold / 100) * limit);
    return currentCount >= thresholdCount;
  })());

  const countMessageText = $derived((() => {
    const unit = maxwords ? 'word' : 'character';
    const units = maxwords ? 'words' : 'characters';

    if (remainingCount < 0) {
      const overCount = Math.abs(remainingCount);
      return `You have ${overCount} ${overCount === 1 ? unit : units} too many`;
    } else if (remainingCount === 0) {
      return `You have 0 ${units} remaining`;
    } else {
      return `You have ${remainingCount} ${remainingCount === 1 ? unit : units} remaining`;
    }
  })());

  const formGroupAttributes = $derived(formGroup?.attributes || {});

  const textareaAttributes = $derived({
    ...attributes,
    ...restProps,
    'aria-describedby': [
      hint ? `${elementId}-hint` : '',
      errorMessage ? `${elementId}-error` : '',
      countId
    ].filter(Boolean).join(' ')
  });

  const LabelTag = $derived(label.isPageHeading ? 'h1' : 'label');
</script>

<div
  class="public-good-character-count form-control w-full {formGroup?.classes || ''}"
  {...formGroupAttributes}
>
  <!-- Label -->
  <svelte:element this={LabelTag}
    class="label {label.classes || ''}"
    for={LabelTag === 'label' ? elementId : undefined}
  >
    <span class="label-text {label.isPageHeading ? 'text-2xl font-bold' : ''}">
      {#if label.html}
        {@html label.html}
      {:else}
        {label.text}
      {/if}
    </span>
  </svelte:element>

  <!-- Hint -->
  {#if hint}
    <div class="label-text-alt text-base-content/70 mb-2" id="{elementId}-hint">
      {hint.text}
    </div>
  {/if}

  <!-- Error Message -->
  {#if errorMessage}
    <div class="label-text-alt text-error mb-2" id="{elementId}-error">
      <span class="font-medium">Error:</span> {errorMessage.text}
    </div>
  {/if}

  <!-- Textarea -->
  <textarea
    id={elementId}
    {name}
    {rows}
    {spellcheck}
    class="textarea textarea-bordered public-good-js-character-count {classes} {errorMessage ? 'textarea-error' : ''}"
    bind:value
    {...textareaAttributes}
  ></textarea>

  <!-- Character/Word Count Display -->
  <div
    class="label-text-alt mt-2 {countMessage?.classes || ''} {isOverLimit ? 'text-error' : showWarning ? 'text-warning' : 'text-base-content/70'}"
    id={countId}
    aria-live="polite"
  >
    {countMessageText}
  </div>
</div>