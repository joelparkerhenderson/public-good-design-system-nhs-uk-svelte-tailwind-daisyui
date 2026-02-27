<script lang="ts">
  import type { CardProps } from '$lib/types.js';

  interface Props extends CardProps {}

  let {
    heading,
    headingHtml,
    headingLevel = 2,
    headingClasses = '',
    description,
    descriptionHtml,
    href,
    clickable = false,
    secondary = false,
    feature = false,
    primary = false,
    topTask = false,
    imgURL,
    imgALT,
    type,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const cardClasses = $derived((() => {
    let base = 'card bg-base-100 shadow-xl';
    if (clickable) base += ' card-compact hover:shadow-2xl transition-shadow cursor-pointer';
    if (secondary) base += ' bg-base-200';
    if (feature) base += ' card-bordered border-primary';
    if (primary) base += ' bg-primary text-primary-content';
    if (topTask) base += ' bg-accent text-accent-content';
    if (type === 'non-urgent') base += ' bg-blue-50 border-blue-200';
    if (type === 'urgent') base += ' bg-red-50 border-red-200';
    if (type === 'emergency') base += ' bg-red-600 text-white';
    return `${base} ${classes}`;
  })());

  const cardAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(clickable && href ? { 'data-clickable': 'true', 'data-href': href } : {})
  });

  const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);

  function handleCardClick(event: MouseEvent) {
    if (clickable && href && (event.target as HTMLElement).tagName !== 'A') {
      window.location.href = href;
    }
  }

  function handleCardKeydown(event: KeyboardEvent) {
    if (clickable && href && (event.key === 'Enter' || event.key === ' ')) {
      event.preventDefault();
      window.location.href = href;
    }
  }
</script>

<!-- svelte-ignore a11y_no_static_element_interactions -->
<!-- svelte-ignore a11y_no_noninteractive_tabindex -->
<div
  class={cardClasses}
  onclick={clickable && href ? handleCardClick : undefined}
  onkeydown={clickable && href ? handleCardKeydown : undefined}
  role={clickable && href ? 'link' : undefined}
  tabindex={clickable && href ? 0 : undefined}
  {...cardAttributes}
>
  {#if imgURL}
    <figure>
      <img src={imgURL} alt={imgALT || ''} class="w-full h-48 object-cover" loading="lazy" />
    </figure>
  {/if}

  <div class="card-body">
    <!-- Heading Section -->
    {#if headingHtml || heading}
      <svelte:element this={HeadingTag} class="card-title {headingClasses}">
        {#if href && !feature}
          <a class="link link-hover" {href}>
            {#if headingHtml}
              {@html headingHtml}
            {:else}
              {heading}
            {/if}
          </a>
        {:else}
          {#if type}
            <span>
              <span class="sr-only">
                {#if type === 'non-urgent'}Non-urgent advice:
                {:else if type === 'urgent'}Urgent advice:
                {:else if type === 'emergency'}Immediate action required:
                {:else}Non-urgent advice:{/if}
              </span>
              {#if headingHtml}
                {@html headingHtml}
              {:else}
                {heading}
              {/if}
            </span>
          {:else}
            {#if headingHtml}
              {@html headingHtml}
            {:else}
              {heading}
            {/if}
          {/if}
        {/if}

        {#if type}
          <svg class="w-5 h-5 ml-2" aria-hidden="true" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z" clip-rule="evenodd" />
          </svg>
        {/if}
      </svelte:element>
    {/if}

    <!-- Description Section -->
    {#if descriptionHtml}
      <div class="card-text">
        {@html descriptionHtml}
      </div>
    {:else if description}
      <p class="card-text">
        {description}
      </p>
    {/if}

    <!-- Primary card chevron icon -->
    {#if primary}
      <div class="card-actions justify-end">
        <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 20 20" aria-hidden="true">
          <circle cx="10" cy="10" r="8" fill="currentColor" opacity="0.1"/>
          <path fill-rule="evenodd" d="M7.21 14.77a.75.75 0 01.02-1.06L11.168 10 7.23 6.29a.75.75 0 111.04-1.08l4.5 4.25a.75.75 0 010 1.08l-4.5 4.25a.75.75 0 01-1.06-.02z" clip-rule="evenodd" />
        </svg>
      </div>
    {/if}
  </div>
</div>