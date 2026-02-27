<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface ErrorItem {
    text?: string;
    html?: string;
    href?: string;
    attributes?: Record<string, string>;
  }

  interface ErrorSummaryProps extends BaseComponentProps {
    titleText?: string;
    titleHtml?: string;
    descriptionText?: string;
    descriptionHtml?: string;
    errorList: ErrorItem[];
  }

  interface Props extends ErrorSummaryProps {}

  let {
    titleText = 'There is a problem',
    titleHtml,
    descriptionText,
    descriptionHtml,
    errorList = [],
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const summaryAttributes = $derived({
    ...attributes,
    ...restProps
  });

  let errorSummaryElement: HTMLElement;

  $effect(() => {
    if (errorSummaryElement && errorList.length > 0) {
      errorSummaryElement.focus();
    }
  });
</script>

<div
  class="public-good-error-summary alert alert-error {classes}"
  aria-labelledby="error-summary-title"
  role="alert"
  tabindex="-1"
  bind:this={errorSummaryElement}
  {...summaryAttributes}
>
  <div class="flex">
    <svg
      class="w-6 h-6 flex-shrink-0 mr-3 mt-0.5"
      fill="currentColor"
      viewBox="0 0 20 20"
      aria-hidden="true"
    >
      <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.28 7.22a.75.75 0 00-1.06 1.06L8.94 10l-1.72 1.72a.75.75 0 101.06 1.06L10 11.06l1.72 1.72a.75.75 0 101.06-1.06L11.06 10l1.72-1.72a.75.75 0 00-1.06-1.06L10 8.94 8.28 7.22z" clip-rule="evenodd" />
    </svg>

    <div class="flex-1">
      <h2 class="public-good-error-summary__title font-bold text-lg mb-3" id="error-summary-title">
        {#if titleHtml}
          {@html titleHtml}
        {:else}
          {titleText}
        {/if}
      </h2>

      <div class="public-good-error-summary__body space-y-3">
        {#if children}
          <p>{@render children()}</p>
        {:else if descriptionHtml}
          <p>{@html descriptionHtml}</p>
        {:else if descriptionText}
          <p>{descriptionText}</p>
        {/if}

        {#if errorList.length > 0}
          <ul class="public-good-error-summary__list list-disc list-inside space-y-1" role="list">
            {#each errorList as item}
              <li>
                {#if item.href}
                  <a
                    class="link link-hover underline font-medium"
                    href={item.href}
                    {...(item.attributes || {})}
                  >
                    {#if item.html}
                      {@html item.html}
                    {:else}
                      {item.text}
                    {/if}
                  </a>
                {:else}
                  {#if item.html}
                    {@html item.html}
                  {:else}
                    {item.text}
                  {/if}
                {/if}
              </li>
            {/each}
          </ul>
        {/if}
      </div>
    </div>
  </div>
</div>