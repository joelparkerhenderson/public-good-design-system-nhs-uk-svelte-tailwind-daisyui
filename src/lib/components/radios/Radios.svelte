<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';
  import ErrorMessage from '../error-message/ErrorMessage.svelte';
  import Hint from '../hint/Hint.svelte';
  import Fieldset from '../fieldset/Fieldset.svelte';

  interface RadioItem {
    text?: string;
    html?: string;
    id?: string;
    value: string;
    checked?: boolean;
    disabled?: boolean;
    hint?: { text?: string; html?: string; classes?: string; attributes?: Record<string, string> };
    conditional?: { html: string };
    divider?: string;
    label?: { classes?: string; attributes?: Record<string, string> };
    attributes?: Record<string, string>;
  }

  interface RadioFieldset {
    legend?: {
      text?: string;
      html?: string;
      classes?: string;
      isPageHeading?: boolean;
    };
    classes?: string;
    attributes?: Record<string, string>;
    describedBy?: string;
  }

  interface RadioHint {
    text?: string;
    html?: string;
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface RadioErrorMessage {
    text?: string;
    html?: string;
    classes?: string;
  }

  interface RadioFormGroup {
    classes?: string;
    attributes?: Record<string, string>;
  }

  interface RadiosProps extends BaseComponentProps {
    name: string;
    items: RadioItem[];
    value?: string;
    idPrefix?: string;
    fieldset?: RadioFieldset;
    hint?: RadioHint;
    errorMessage?: RadioErrorMessage;
    formGroup?: RadioFormGroup;
  }

  interface Props extends RadiosProps {}

  let {
    name,
    items = [],
    value = $bindable(),
    idPrefix,
    fieldset,
    hint,
    errorMessage,
    formGroup,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const prefix = $derived(idPrefix || name);
  const hintId = $derived(hint ? `${prefix}-hint` : undefined);
  const errorId = $derived(errorMessage ? `${prefix}-error` : undefined);

  const fieldsetDescribedBy = $derived((() => {
    const parts: string[] = [];
    if (fieldset?.describedBy) parts.push(fieldset.describedBy);
    if (hintId) parts.push(hintId);
    if (errorId) parts.push(errorId);
    return parts.length > 0 ? parts.join(' ') : undefined;
  })());

  const isConditional = $derived(items.some(item => item.conditional?.html));

  function handleRadioChange(itemValue: string) {
    value = itemValue;
  }

  function getItemId(item: RadioItem, index: number): string {
    return item.id || `${prefix}${index > 0 ? `-${index + 1}` : ''}`;
  }

  function getItemHintId(item: RadioItem, index: number): string {
    return `${getItemId(item, index)}-item-hint`;
  }

  function getConditionalId(item: RadioItem, index: number): string {
    return `conditional-${getItemId(item, index)}`;
  }

  function isItemChecked(item: RadioItem): boolean {
    if (item.checked !== undefined) return item.checked;
    if (value !== undefined && item.value === value) return item.checked !== false;
    return false;
  }

  const formGroupAttributes = $derived(formGroup?.attributes || {});

  const radiosAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

{#snippet radioItems()}
  {#each items as item, index}
    {#if item.divider}
      <div class="public-good-radios__divider text-sm font-medium text-base-content/70 my-4">
        {item.divider}
      </div>
    {:else}
      {@const itemId = getItemId(item, index)}
      {@const itemHintId = item.hint ? getItemHintId(item, index) : undefined}
      {@const conditionalId = item.conditional ? getConditionalId(item, index) : undefined}
      {@const checked = isItemChecked(item)}

      <div class="public-good-radios__item">
        <label class="cursor-pointer label justify-start gap-3 p-0">
          <input
            class="radio public-good-radios__input"
            type="radio"
            id={itemId}
            {name}
            value={item.value}
            checked={checked}
            disabled={item.disabled}
            onchange={() => handleRadioChange(item.value)}
            aria-describedby={itemHintId}
            aria-controls={conditionalId}
            {...(item.attributes || {})}
          />

          <div class="flex-1">
            <div class="public-good-radios__label label-text {item.label?.classes || ''}" {...(item.label?.attributes || {})}>
              {#if item.html}
                {@html item.html}
              {:else}
                {item.text}
              {/if}
            </div>

            {#if item.hint}
              <div
                class="public-good-radios__hint text-sm text-base-content/70 mt-1 {item.hint.classes || ''}"
                id={itemHintId}
                {...(item.hint.attributes || {})}
              >
                {#if item.hint.html}
                  {@html item.hint.html}
                {:else}
                  {item.hint.text}
                {/if}
              </div>
            {/if}
          </div>
        </label>

        {#if item.conditional}
          <div
            class="public-good-radios__conditional ml-6 mt-3 p-3 bg-base-200 rounded {checked ? '' : 'hidden'}"
            id={conditionalId}
          >
            {@html item.conditional.html}
          </div>
        {/if}
      </div>
    {/if}
  {/each}
{/snippet}

<div
  class="public-good-form-group form-control {errorMessage ? 'public-good-form-group--error' : ''} {formGroup?.classes || ''}"
  {...formGroupAttributes}
>
  {#if fieldset}
    <Fieldset
      legend={fieldset.legend}
      describedBy={fieldsetDescribedBy}
      classes={fieldset.classes}
      attributes={fieldset.attributes}
    >
      {#if hint}
        <Hint id={hintId} text={hint.text} html={hint.html} classes={hint.classes} attributes={hint.attributes} />
      {/if}

      {#if errorMessage}
        <ErrorMessage id={errorId} text={errorMessage.text} html={errorMessage.html} classes={errorMessage.classes} />
      {/if}

      <div
        class="public-good-radios space-y-3 {classes} {isConditional ? 'public-good-radios--conditional' : ''}"
        {...radiosAttributes}
      >
        {@render radioItems()}
      </div>
    </Fieldset>
  {:else}
    {#if hint}
      <Hint id={hintId} text={hint.text} html={hint.html} classes={hint.classes} attributes={hint.attributes} />
    {/if}

    {#if errorMessage}
      <ErrorMessage id={errorId} text={errorMessage.text} html={errorMessage.html} classes={errorMessage.classes} />
    {/if}

    <div
      class="public-good-radios space-y-3 {classes} {isConditional ? 'public-good-radios--conditional' : ''}"
      {...radiosAttributes}
    >
      {@render radioItems()}
    </div>
  {/if}

  {#if children}
    {@render children()}
  {/if}
</div>