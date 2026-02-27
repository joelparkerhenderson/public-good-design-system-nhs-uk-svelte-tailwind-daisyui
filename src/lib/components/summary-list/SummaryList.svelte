<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface SummaryListAction {
    href: string;
    text?: string;
    html?: string;
    visuallyHiddenText?: string;
    attributes?: Record<string, string>;
  }

  interface SummaryListActions {
    items: SummaryListAction[];
    classes?: string;
  }

  interface SummaryListKey {
    text?: string;
    html?: string;
    classes?: string;
  }

  interface SummaryListValue {
    text?: string;
    html?: string;
    classes?: string;
  }

  interface SummaryListRow {
    key: SummaryListKey;
    value: SummaryListValue;
    actions?: SummaryListActions;
    classes?: string;
  }

  interface SummaryListProps extends BaseComponentProps {
    rows: SummaryListRow[];
  }

  interface Props extends SummaryListProps {}

  let {
    rows = [],
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const anyRowHasActions = $derived(
    rows.some(row => row.actions?.items && row.actions.items.length > 0)
  );

  const summaryListAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<dl
  class="public-good-summary-list grid gap-4 {classes}"
  {...summaryListAttributes}
>
  {#each rows as row}
    {#if row}
      <div class="public-good-summary-list__row grid {anyRowHasActions ? 'grid-cols-1 md:grid-cols-3' : 'grid-cols-1 md:grid-cols-2'} gap-2 md:gap-4 py-3 border-b border-base-300 last:border-b-0 {row.classes || ''}">
        <dt class="public-good-summary-list__key font-semibold text-base-content {row.key.classes || ''}">
          {#if row.key.html}
            {@html row.key.html}
          {:else}
            {row.key.text}
          {/if}
        </dt>

        <dd class="public-good-summary-list__value text-base-content {row.value.classes || ''}">
          {#if row.value.html}
            {@html row.value.html}
          {:else}
            {row.value.text}
          {/if}
        </dd>

        {#if row.actions?.items && row.actions.items.length > 0}
          <dd class="public-good-summary-list__actions {row.actions.classes || ''}">
            {#if row.actions.items.length === 1}
              {@const action = row.actions.items[0]}
              <a
                href={action.href}
                class="link link-primary text-sm"
                {...(action.attributes || {})}
              >
                {#if action.html}
                  {@html action.html}
                {:else}
                  {action.text}
                {/if}
                {#if action.visuallyHiddenText}
                  <span class="sr-only"> {action.visuallyHiddenText}</span>
                {/if}
              </a>
            {:else}
              <ul class="public-good-summary-list__actions-list space-y-1">
                {#each row.actions.items as action}
                  <li class="public-good-summary-list__actions-list-item">
                    <a
                      href={action.href}
                      class="link link-primary text-sm"
                      {...(action.attributes || {})}
                    >
                      {#if action.html}
                        {@html action.html}
                      {:else}
                        {action.text}
                      {/if}
                      {#if action.visuallyHiddenText}
                        <span class="sr-only"> {action.visuallyHiddenText}</span>
                      {/if}
                    </a>
                  </li>
                {/each}
              </ul>
            {/if}
          </dd>
        {/if}
      </div>
    {/if}
  {/each}

  {#if children}
    {@render children()}
  {/if}
</dl>