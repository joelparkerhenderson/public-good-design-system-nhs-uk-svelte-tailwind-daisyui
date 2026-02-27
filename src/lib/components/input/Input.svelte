<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';
  import ErrorMessage from '../error-message/ErrorMessage.svelte';
  import Hint from '../hint/Hint.svelte';

  interface InputLabel {
    text?: string;
    html?: string;
    classes?: string;
    isPageHeading?: boolean;
    attributes?: Record<string, string>;
  }

  interface InputHint {
    text?: string;
    html?: string;
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface InputErrorMessage {
    text?: string;
    html?: string;
    classes?: string;
  }

  interface InputFormGroup {
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface InputProps extends BaseComponentProps {
    id?: string;
    name: string;
    type?: 'text' | 'email' | 'password' | 'tel' | 'url' | 'search' | 'number';
    value?: string;
    label: InputLabel;
    hint?: InputHint;
    errorMessage?: InputErrorMessage;
    formGroup?: InputFormGroup;
    describedBy?: string;
    spellcheck?: boolean;
    autocomplete?: string;
    pattern?: string;
    inputmode?: 'none' | 'text' | 'tel' | 'url' | 'email' | 'numeric' | 'decimal' | 'search';
    prefix?: string;
    suffix?: string;
    disabled?: boolean;
    readonly?: boolean;
    required?: boolean;
    placeholder?: string;
  }

  interface Props extends InputProps {}

  let {
    id,
    name,
    type = 'text',
    value = $bindable(''),
    label,
    hint,
    errorMessage,
    formGroup,
    describedBy,
    spellcheck,
    autocomplete,
    pattern,
    inputmode,
    prefix,
    suffix,
    disabled,
    readonly,
    required,
    placeholder,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const inputId = $derived(id || name);
  const hintId = $derived(hint ? `${inputId}-hint` : undefined);
  const errorId = $derived(errorMessage ? `${inputId}-error` : undefined);

  const ariaDescribedBy = $derived((() => {
    const parts = [];
    if (describedBy) parts.push(describedBy);
    if (hintId) parts.push(hintId);
    if (errorId) parts.push(errorId);
    return parts.length > 0 ? parts.join(' ') : undefined;
  })());

  const formGroupAttributes = $derived(formGroup?.attributes || {});

  const inputAttributes = $derived({
    ...attributes,
    ...restProps,
    'aria-describedby': ariaDescribedBy,
    ...(spellcheck !== undefined ? { spellcheck } : {}),
    ...(autocomplete ? { autocomplete } : {}),
    ...(pattern ? { pattern } : {}),
    ...(inputmode ? { inputmode } : {})
  });
</script>

<div
  class="public-good-form-group form-control {errorMessage ? 'public-good-form-group--error' : ''} {formGroup?.classes || ''}"
  {...formGroupAttributes}
>
  <!-- Label -->
  {#if label.isPageHeading}
    <h1 class="label-text text-3xl font-bold {label.classes || ''}" {...(label.attributes || {})}>
      <label for={inputId}>
        {#if label.html}
          {@html label.html}
        {:else}
          {label.text}
        {/if}
      </label>
    </h1>
  {:else}
    <label class="label {label.classes || ''}" for={inputId} {...(label.attributes || {})}>
      <span class="label-text">
        {#if label.html}
          {@html label.html}
        {:else}
          {label.text}
        {/if}
      </span>
    </label>
  {/if}

  <!-- Hint -->
  {#if hint}
    <Hint
      id={hintId}
      text={hint.text}
      html={hint.html}
      classes={hint.classes}
      attributes={hint.attributes}
    />
  {/if}

  <!-- Error Message -->
  {#if errorMessage}
    <ErrorMessage
      id={errorId}
      text={errorMessage.text}
      html={errorMessage.html}
      classes={errorMessage.classes}
    />
  {/if}

  <!-- Input with optional prefix/suffix wrapper -->
  {#if prefix || suffix}
    <div class="public-good-input__wrapper flex items-center">
      {#if prefix}
        <div class="public-good-input__prefix px-3 py-2 bg-base-200 border border-r-0 border-base-300 rounded-l-lg text-sm" aria-hidden="true">
          {prefix}
        </div>
      {/if}

      <input
        class="input input-bordered public-good-input {classes} {errorMessage ? 'input-error' : ''} {prefix ? 'rounded-l-none' : ''} {suffix ? 'rounded-r-none' : ''}"
        id={inputId}
        {name}
        {type}
        bind:value
        {disabled}
        {readonly}
        {required}
        {placeholder}
        {...inputAttributes}
      />

      {#if suffix}
        <div class="public-good-input__suffix px-3 py-2 bg-base-200 border border-l-0 border-base-300 rounded-r-lg text-sm" aria-hidden="true">
          {suffix}
        </div>
      {/if}
    </div>
  {:else}
    <input
      class="input input-bordered public-good-input {classes} {errorMessage ? 'input-error' : ''}"
      id={inputId}
      {name}
      {type}
      bind:value
      {disabled}
      {readonly}
      {required}
      {placeholder}
      {...inputAttributes}
    />
  {/if}

  {#if children}
    {@render children()}
  {/if}
</div>