<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface DateInputItem {
    name: string;
    label?: string;
    id?: string;
    classes?: string;
    value?: string;
    inputmode?: string;
    autocomplete?: string;
    pattern?: string;
    attributes?: Record<string, string>;
  }

  interface DateInputProps extends BaseComponentProps {
    id?: string;
    namePrefix?: string;
    values?: {
      day?: string;
      month?: string;
      year?: string;
    };
    items?: DateInputItem[];
    fieldset?: {
      legend: {
        text?: string;
        html?: string;
        classes?: string;
        isPageHeading?: boolean;
      };
      classes?: string;
      describedBy?: string;
    };
    hint?: {
      text?: string;
      html?: string;
      classes?: string;
    };
    errorMessage?: {
      text?: string;
      html?: string;
      classes?: string;
    };
    formGroup?: {
      classes?: string;
      attributes?: Record<string, string>;
    };
  }

  interface Props extends DateInputProps {}

  let {
    id,
    namePrefix,
    values = {},
    items,
    fieldset,
    hint,
    errorMessage,
    formGroup,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const dateInputItems = $derived(items || [
    { name: "day", classes: "w-16", value: values.day || '', inputmode: "numeric", pattern: "[0-9]*" },
    { name: "month", classes: "w-16", value: values.month || '', inputmode: "numeric", pattern: "[0-9]*" },
    { name: "year", classes: "w-20", value: values.year || '', inputmode: "numeric", pattern: "[0-9]*" }
  ]);

  const componentId = $derived(id || 'date-input');
  const hintId = $derived(hint ? `${componentId}-hint` : '');
  const errorId = $derived(errorMessage ? `${componentId}-error` : '');

  const describedBy = $derived((() => {
    const parts = [
      fieldset?.describedBy || '',
      hintId,
      errorId
    ].filter(Boolean);
    return parts.length > 0 ? parts.join(' ') : undefined;
  })());

  const formGroupAttributes = $derived({
    ...(formGroup?.attributes || {}),
    ...restProps
  });

  const getInputName = (itemName: string) =>
    namePrefix ? `${namePrefix}[${itemName}]` : itemName;

  const getInputId = (item: DateInputItem) =>
    item.id || `${componentId}-${item.name}`;

  const getInputLabel = (item: DateInputItem) =>
    item.label || item.name.charAt(0).toUpperCase() + item.name.slice(1);
</script>

{#snippet dateFields()}
  <div
    class="public-good-date-input__fields flex gap-4 {classes}"
    id={componentId}
    {...attributes}
  >
    {#each dateInputItems as item}
      <div class="public-good-date-input__item form-control">
        <label class="label pb-1" for={getInputId(item)}>
          <span class="label-text text-sm public-good-date-input__label">
            {getInputLabel(item)}
          </span>
        </label>
        <input
          type="text"
          id={getInputId(item)}
          name={getInputName(item.name)}
          value={item.value}
          class="input input-bordered public-good-date-input__input {item.classes || ''} {errorMessage ? 'input-error' : ''}"
          inputmode={item.inputmode || 'numeric'}
          autocomplete={item.autocomplete}
          pattern={item.pattern}
          {...(item.attributes || {})}
        />
      </div>
    {/each}
  </div>
{/snippet}

{#snippet hintBlock()}
  {#if hint}
    <div class="label-text-alt text-base-content/70 {hint.classes || ''}" id={hintId}>
      {#if hint.html}
        {@html hint.html}
      {:else}
        {hint.text}
      {/if}
    </div>
  {/if}
{/snippet}

{#snippet errorBlock()}
  {#if errorMessage}
    <div class="label-text-alt text-error {errorMessage.classes || ''}" id={errorId}>
      <span class="font-medium">Error:</span>
      {#if errorMessage.html}
        {@html errorMessage.html}
      {:else}
        {errorMessage.text}
      {/if}
    </div>
  {/if}
{/snippet}

<div
  class="public-good-date-input form-control {errorMessage ? 'nhsuk-form-group--error' : ''} {formGroup?.classes || ''}"
  {...formGroupAttributes}
>
  {#if fieldset}
    <fieldset
      class="space-y-4 {fieldset.classes || ''}"
      aria-describedby={describedBy}
    >
      {#if fieldset.legend}
        {#if fieldset.legend.isPageHeading}
          <legend class="label-text text-base font-medium {fieldset.legend.classes || ''}">
            <h1 class="text-2xl font-bold">
              {#if fieldset.legend.html}
                {@html fieldset.legend.html}
              {:else}
                {fieldset.legend.text}
              {/if}
            </h1>
          </legend>
        {:else}
          <legend class="label-text text-base font-medium {fieldset.legend.classes || ''}">
            {#if fieldset.legend.html}
              {@html fieldset.legend.html}
            {:else}
              {fieldset.legend.text}
            {/if}
          </legend>
        {/if}
      {/if}

      {@render hintBlock()}
      {@render errorBlock()}
      {@render dateFields()}
    </fieldset>
  {:else}
    {@render hintBlock()}
    {@render errorBlock()}
    <div aria-describedby={describedBy}>
      {@render dateFields()}
    </div>
  {/if}
</div>