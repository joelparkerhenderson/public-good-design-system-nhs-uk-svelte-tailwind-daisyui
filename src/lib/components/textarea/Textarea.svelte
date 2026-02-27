<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';
  import Label from '../label/Label.svelte';
  import Hint from '../hint/Hint.svelte';
  import ErrorMessage from '../error-message/ErrorMessage.svelte';

  interface TextareaLabel {
    text?: string;
    html?: string;
    classes?: string;
    isPageHeading?: boolean;
    attributes?: Record<string, string>;
  }

  interface TextareaHint {
    text?: string;
    html?: string;
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface TextareaErrorMessage {
    text?: string;
    html?: string;
    classes?: string;
  }

  interface TextareaFormGroup {
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface TextareaProps extends BaseComponentProps {
    id?: string;
    name: string;
    value?: string;
    rows?: number;
    label: TextareaLabel;
    hint?: TextareaHint;
    errorMessage?: TextareaErrorMessage;
    formGroup?: TextareaFormGroup;
    describedBy?: string;
    disabled?: boolean;
    readonly?: boolean;
    required?: boolean;
    placeholder?: string;
    autocomplete?: string;
    maxlength?: number;
    cols?: number;
  }

  interface Props extends TextareaProps {}

  let {
    id,
    name,
    value = $bindable(''),
    rows = 5,
    label,
    hint,
    errorMessage,
    formGroup,
    describedBy,
    disabled = false,
    readonly = false,
    required = false,
    placeholder,
    autocomplete,
    maxlength,
    cols,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const textareaId = $derived(id || name);
  const hintId = $derived(hint ? `${textareaId}-hint` : undefined);
  const errorId = $derived(errorMessage ? `${textareaId}-error` : undefined);

  const ariaDescribedBy = $derived((() => {
    const ids: string[] = [];
    if (describedBy) ids.push(describedBy);
    if (hintId) ids.push(hintId);
    if (errorId) ids.push(errorId);
    return ids.length > 0 ? ids.join(' ') : undefined;
  })());

  const textareaAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(autocomplete ? { autocomplete } : {}),
    ...(placeholder ? { placeholder } : {}),
    ...(maxlength ? { maxlength } : {}),
    ...(cols ? { cols } : {})
  });
</script>

<div
  class="public-good-textarea-form-group form-control w-full {errorMessage ? 'form-control-error' : ''} {formGroup?.classes || ''}"
  {...(formGroup?.attributes || {})}
>
  {#if label}
    <Label
      for={textareaId}
      text={label.text}
      html={label.html}
      classes="label {label.classes || ''}"
      isPageHeading={label.isPageHeading}
      attributes={label.attributes}
    />
  {/if}

  {#if hint}
    <Hint
      id={hintId}
      text={hint.text}
      html={hint.html}
      classes="text-sm text-base-content/70 mb-2 {hint.classes || ''}"
      attributes={hint.attributes}
    />
  {/if}

  {#if errorMessage}
    <ErrorMessage
      id={errorId}
      text={errorMessage.text}
      html={errorMessage.html}
      classes="text-sm text-error mb-2 {errorMessage.classes || ''}"
    />
  {/if}

  <textarea
    class="public-good-textarea textarea textarea-bordered w-full {errorMessage ? 'textarea-error border-error focus:border-error' : 'focus:border-primary'} {classes}"
    id={textareaId}
    {name}
    bind:value
    {rows}
    {disabled}
    {readonly}
    {required}
    aria-describedby={ariaDescribedBy}
    {...textareaAttributes}
  ></textarea>

  {#if children}
    {@render children()}
  {/if}
</div>

<style>
  .public-good-textarea {
    resize: vertical;
  }
</style>