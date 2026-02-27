<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface TabPanel {
    text?: string;
    html?: string;
    attributes?: Record<string, string>;
  }

  interface TabItem {
    label: string;
    id?: string;
    panel: TabPanel;
    attributes?: Record<string, string>;
  }

  interface TabsProps extends BaseComponentProps {
    items: TabItem[];
    title?: string;
    idPrefix?: string;
    id?: string;
  }

  interface Props extends TabsProps {}

  let {
    items = [],
    title = 'Contents',
    idPrefix = 'tab',
    id,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  let activeTabIndex = $state(0);

  const tabsAttributes = $derived({
    ...attributes,
    ...restProps
  });

  function generateTabId(item: TabItem, index: number): string {
    return item.id || `${idPrefix}-${index + 1}`;
  }

  function handleTabClick(index: number, event: Event) {
    event.preventDefault();
    activeTabIndex = index;
  }

  function handleKeydown(event: KeyboardEvent, index: number) {
    switch (event.key) {
      case 'ArrowLeft':
        event.preventDefault();
        activeTabIndex = index > 0 ? index - 1 : items.length - 1;
        break;
      case 'ArrowRight':
        event.preventDefault();
        activeTabIndex = index < items.length - 1 ? index + 1 : 0;
        break;
      case 'Home':
        event.preventDefault();
        activeTabIndex = 0;
        break;
      case 'End':
        event.preventDefault();
        activeTabIndex = items.length - 1;
        break;
    }
  }
</script>

<div
  {id}
  class="public-good-tabs tabs tabs-boxed bg-base-100 {classes}"
  {...tabsAttributes}
>
  <h2 class="public-good-tabs__title text-lg font-semibold mb-4 md:hidden">
    {title}
  </h2>

  {#if items.length > 0}
    <div class="tabs-list" role="tablist">
      {#each items as item, index}
        {@const tabId = generateTabId(item, index)}
        <button
          class="tab tab-bordered {activeTabIndex === index ? 'tab-active' : ''}"
          role="tab"
          aria-selected={activeTabIndex === index}
          aria-controls="{tabId}-panel"
          id="{tabId}-tab"
          tabindex={activeTabIndex === index ? 0 : -1}
          onclick={(e: Event) => handleTabClick(index, e)}
          onkeydown={(e: KeyboardEvent) => handleKeydown(e, index)}
          {...(item.attributes || {})}
        >
          {item.label}
        </button>
      {/each}
    </div>

    <div class="tab-panels mt-4">
      {#each items as item, index}
        {@const tabId = generateTabId(item, index)}
        <div
          class="public-good-tabs__panel tab-panel {activeTabIndex === index ? 'block' : 'hidden'}"
          id="{tabId}-panel"
          role="tabpanel"
          aria-labelledby="{tabId}-tab"
          tabindex="0"
          {...(item.panel.attributes || {})}
        >
          {#if item.panel.html}
            {@html item.panel.html}
          {:else if item.panel.text}
            <p>{item.panel.text}</p>
          {/if}
        </div>
      {/each}
    </div>
  {/if}

  {#if children}
    {@render children()}
  {/if}
</div>

<style>
  .tab-panel {
    min-height: 200px;
    padding: 1rem;
    background: white;
    border: 1px solid #e5e7eb;
    border-top: none;
    border-radius: 0 0 0.5rem 0.5rem;
  }

  .tab-panel:focus {
    outline: 2px solid #2563eb;
    outline-offset: 2px;
  }

  @media (max-width: 768px) {
    .tabs-list {
      flex-direction: column;
      align-items: stretch;
    }

    .tab {
      justify-content: flex-start;
      text-align: left;
    }
  }
</style>