<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface TableCell {
    text?: string;
    html?: string;
    header?: string;
    classes?: string;
    format?: 'numeric' | 'sort-ascending' | 'sort-descending';
    colspan?: number;
    rowspan?: number;
    attributes?: Record<string, string>;
  }

  interface TableHead {
    text?: string;
    html?: string;
    classes?: string;
    format?: 'numeric' | 'sort-ascending' | 'sort-descending';
    colspan?: number;
    rowspan?: number;
    attributes?: Record<string, string>;
  }

  interface TablesProps extends BaseComponentProps {
    rows: TableCell[][];
    head?: TableHead[];
    caption?: string;
    captionClasses?: string;
    tableClasses?: string;
    responsive?: boolean;
    firstCellIsHeader?: boolean;
    panel?: boolean;
    panelClasses?: string;
    heading?: string;
    headingLevel?: 1 | 2 | 3 | 4 | 5 | 6;
  }

  interface Props extends TablesProps {}

  let {
    rows = [],
    head,
    caption,
    captionClasses = '',
    tableClasses = '',
    responsive = false,
    firstCellIsHeader = false,
    panel = false,
    panelClasses = '',
    heading,
    headingLevel = 3,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const tableAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(responsive ? { role: 'table' } : {})
  });

  const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);
</script>

{#snippet tableContent()}
  <table
    class="public-good-table table {responsive ? 'table-xs md:table-md' : 'table-md'} {tableClasses} {classes}"
    {...tableAttributes}
  >
    {#if caption}
      <caption class="public-good-table__caption caption-top text-left font-semibold mb-3 {captionClasses}">
        {caption}
      </caption>
    {/if}

    {#if head}
      <thead class="public-good-table__head" role={responsive ? 'rowgroup' : undefined}>
        <tr role={responsive ? 'row' : undefined}>
          {#each head as item}
            <th
              scope="col"
              class="public-good-table__header {item.format ? `table-header--${item.format}` : ''} {item.classes || ''}"
              colspan={item.colspan}
              rowspan={item.rowspan}
              role={responsive ? 'columnheader' : undefined}
              {...(item.attributes || {})}
            >
              {#if item.html}
                {@html item.html}
              {:else}
                {item.text}
              {/if}
            </th>
          {/each}
        </tr>
      </thead>
    {/if}

    <tbody class="public-good-table__body">
      {#each rows as row}
        <tr class="public-good-table__row" role={responsive ? 'row' : undefined}>
          {#each row as cell, cellIndex}
            {#if cellIndex === 0 && firstCellIsHeader}
              <th
                scope="row"
                class="public-good-table__header font-semibold {cell.classes || ''}"
                role={responsive ? 'rowheader' : undefined}
                colspan={cell.colspan}
                rowspan={cell.rowspan}
                {...(cell.attributes || {})}
              >
                {#if responsive && cell.header}
                  <span class="public-good-table-responsive__heading text-xs font-normal opacity-70 block md:hidden" aria-hidden="true">
                    {cell.header}
                  </span>
                {/if}
                {#if cell.html}
                  {@html cell.html}
                {:else}
                  {cell.text}
                {/if}
              </th>
            {:else}
              <td
                class="public-good-table__cell {cell.format ? `table-cell--${cell.format}` : ''} {cell.classes || ''}"
                role={responsive ? 'cell' : undefined}
                colspan={cell.colspan}
                rowspan={cell.rowspan}
                {...(cell.attributes || {})}
              >
                {#if responsive && cell.header}
                  <span class="public-good-table-responsive__heading text-xs font-normal opacity-70 block md:hidden" aria-hidden="true">
                    {cell.header}
                  </span>
                {/if}
                {#if cell.html}
                  {@html cell.html}
                {:else}
                  {cell.text}
                {/if}
              </td>
            {/if}
          {/each}
        </tr>
      {/each}
    </tbody>
  </table>
{/snippet}

{#if panel}
  <div class="public-good-table__panel card bg-base-100 shadow-sm border {panelClasses}">
    {#if heading}
      <svelte:element this={HeadingTag} class="public-good-table__heading card-title text-lg font-bold p-6 pb-4">
        {heading}
      </svelte:element>
    {/if}

    <div class="card-body pt-0">
      <div class="overflow-x-auto">
        {@render tableContent()}
      </div>
    </div>
  </div>
{:else}
  <div class="overflow-x-auto">
    {@render tableContent()}
  </div>
{/if}

{#if children}
  {@render children()}
{/if}

<style>
  .table-header--numeric,
  .table-cell--numeric {
    text-align: right;
  }

  .table-header--sort-ascending::after {
    content: " ↑";
    opacity: 0.7;
  }

  .table-header--sort-descending::after {
    content: " ↓";
    opacity: 0.7;
  }
</style>