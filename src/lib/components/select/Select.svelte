<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';
  import ErrorMessage from '../error-message/ErrorMessage.svelte';
  import Hint from '../hint/Hint.svelte';

  interface SelectItem {
    text: string;
    value?: string;
    selected?: boolean;
    disabled?: boolean;
    attributes?: Record<string, string>;
  }

  interface SelectLabel {
    text?: string;
    html?: string;
    classes?: string;
    isPageHeading?: boolean;
    attributes?: Record<string, string>;
  }

  interface SelectHint {
    text?: string;
    html?: string;
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface SelectErrorMessage {
    text?: string;
    html?: string;
    classes?: string;
  }

  interface SelectFormGroup {
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface SelectProps extends BaseComponentProps {
    id?: string;
    name: string;
    items: SelectItem[];
    value?: string;
    label: SelectLabel;
    hint?: SelectHint;
    errorMessage?: SelectErrorMessage;
    formGroup?: SelectFormGroup;
    describedBy?: string;
    disabled?: boolean;
  }

  interface Props extends SelectProps {}

  let {
    id,
    name,
    items = [],
    value = $bindable(''),
    label,
    hint,
    errorMessage,
    formGroup,
    describedBy,
    disabled,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const selectId = $derived(id || name);
  const hintId = $derived(hint ? `${selectId}-hint` : undefined);
  const errorId = $derived(errorMessage ? `${selectId}-error` : undefined);

  const ariaDescribedBy = $derived((() => {
    const parts: string[] = [];
    if (describedBy) parts.push(describedBy);
    if (hintId) parts.push(hintId);
    if (errorId) parts.push(errorId);
    return parts.length > 0 ? parts.join(' ') : undefined;
  })());

  const formGroupAttributes = $derived(formGroup?.attributes || {});

  const selectAttributes = $derived({
    ...attributes,
    ...restProps,
    'aria-describedby': ariaDescribedBy
  });

  function getEffectiveValue(item: SelectItem): string {
    return item.value !== undefined ? item.value : item.text;
  }
</script>

<div
  class="public-good-form-group form-control {errorMessage ? 'public-good-form-group--error' : ''} {formGroup?.classes || ''}"
  {...formGroupAttributes}
>
  {#if label.isPageHeading}
    <h1 class="label-text text-3xl font-bold {label.classes || ''}" {...(label.attributes || {})}>
      <label for={selectId}>
        {#if label.html}
          {@html label.html}
        {:else}
          {label.text}
        {/if}
      </label>
    </h1>
  {:else}
    <label class="label {label.classes || ''}" for={selectId} {...(label.attributes || {})}>
      <span class="label-text">
        {#if label.html}
          {@html label.html}
        {:else}
          {label.text}
        {/if}
      </span>
    </label>
  {/if}

  {#if hint}
    <Hint id={hintId} text={hint.text} html={hint.html} classes={hint.classes} attributes={hint.attributes} />
  {/if}

  {#if errorMessage}
    <ErrorMessage id={errorId} text={errorMessage.text} html={errorMessage.html} classes={errorMessage.classes} />
  {/if}

  <select
    class="select select-bordered public-good-select {classes} {errorMessage ? 'select-error' : ''}"
    id={selectId}
    {name}
    bind:value
    {disabled}
    {...selectAttributes}
  >
    {#each items as item}
      <option
        value={getEffectiveValue(item)}
        disabled={item.disabled}
        {...(item.attributes || {})}
      >
        {item.text}
      </option>
    {/each}
  </select>

  {#if children}
    {@render children()}
  {/if}
</div>