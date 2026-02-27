<script lang="ts">
  import type { CheckboxesProps } from '$lib/types.js';

  interface Props extends CheckboxesProps {}

  let {
    name,
    items = [],
    describedBy,
    fieldset,
    hint,
    errorMessage,
    formGroup,
    idPrefix,
    exclusive = false,
    exclusiveGroup,
    values = $bindable([]),
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const checkedValues = $derived(new Set(values));

  const getItemId = (item: any, index: number) => {
    if (item.id) return item.id;
    const prefix = idPrefix || name;
    return `${prefix}-${index}`;
  };

  function handleCheckboxChange(value: string, checked: boolean, item: any) {
    let newValues = [...values];

    if (checked) {
      if (item.exclusive) {
        if (exclusiveGroup || item.exclusiveGroup) {
          newValues = newValues.filter(v =>
            !items.some(other =>
              other.value === v &&
              other.exclusiveGroup === (item.exclusiveGroup || exclusiveGroup) &&
              other.value !== value
            )
          );
        } else {
          newValues = [];
        }
      } else {
        newValues = newValues.filter(v =>
          !items.some(other =>
            other.value === v &&
            other.exclusive &&
            (!exclusiveGroup || !item.exclusiveGroup || other.exclusiveGroup === item.exclusiveGroup)
          )
        );
      }
      if (!newValues.includes(value)) {
        newValues.push(value);
      }
    } else {
      newValues = newValues.filter(v => v !== value);
    }

    values = newValues;
  }

  const formGroupAttributes = $derived({
    ...(formGroup?.attributes || {}),
    ...restProps
  });

  const fieldsetDescribedBy = $derived((() => {
    const parts = [
      describedBy,
      hint ? `${name}-hint` : '',
      errorMessage ? `${name}-error` : ''
    ].filter(Boolean);
    return parts.length > 0 ? parts.join(' ') : undefined;
  })());
</script>

{#snippet checkboxItems()}
  {#each items as item, index}
    {#if item.divider}
      <div class="divider text-base-content/50 text-sm">{item.divider}</div>
    {:else}
      <div class="form-control">
        <label class="label cursor-pointer justify-start gap-3">
          <input
            type="checkbox"
            id={getItemId(item, index)}
            name={item.name || name}
            value={item.value}
            class="checkbox checkbox-primary {errorMessage ? 'checkbox-error' : ''}"
            checked={checkedValues.has(item.value)}
            disabled={item.disabled}
            aria-describedby={item.hint ? `${getItemId(item, index)}-hint` : undefined}
            onchange={(e: Event) => handleCheckboxChange(item.value, (e.target as HTMLInputElement).checked, item)}
            {...(item.attributes || {})}
          />

          <div class="flex-1">
            <span class="label-text">
              {#if item.html}
                {@html item.html}
              {:else}
                {item.text}
              {/if}
            </span>

            {#if item.hint}
              <div class="label-text-alt text-base-content/70 mt-1" id="{getItemId(item, index)}-hint">
                {item.hint.text}
              </div>
            {/if}
          </div>
        </label>

        <!-- Conditional content -->
        {#if item.conditional && checkedValues.has(item.value)}
          <div class="ml-8 mt-3 p-3 bg-base-200 rounded">
            {@html item.conditional.html}
          </div>
        {/if}
      </div>
    {/if}
  {/each}
{/snippet}

<div
  class="public-good-checkboxes form-control w-full {formGroup?.classes || ''}"
  {...formGroupAttributes}
>
  {#if fieldset?.legend}
    <fieldset class="space-y-4" aria-describedby={fieldsetDescribedBy}>
      {#if fieldset.legend.isPageHeading}
        <legend class="label-text text-base font-medium {fieldset.legend.classes || ''}">
          <h1 class="text-2xl font-bold">
            {fieldset.legend.text}
          </h1>
        </legend>
      {:else}
        <legend class="label-text text-base font-medium {fieldset.legend.classes || ''}">
          {fieldset.legend.text}
        </legend>
      {/if}

      {#if hint}
        <div class="label-text-alt text-base-content/70" id="{name}-hint">
          {hint.text}
        </div>
      {/if}

      {#if errorMessage}
        <div class="label-text-alt text-error" id="{name}-error">
          <span class="font-medium">Error:</span> {errorMessage.text}
        </div>
      {/if}

      <div class="space-y-3 {classes}" {...attributes}>
        {@render checkboxItems()}
      </div>
    </fieldset>
  {:else}
    <div class="space-y-3 {classes}" {...attributes} aria-describedby={describedBy}>
      {@render checkboxItems()}
    </div>
  {/if}
</div>