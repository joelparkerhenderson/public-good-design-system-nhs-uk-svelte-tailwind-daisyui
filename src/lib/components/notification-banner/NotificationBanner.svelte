<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface NotificationBannerProps extends BaseComponentProps {
    type?: 'success' | 'warning' | 'info' | 'error';
    titleText?: string;
    titleHtml?: string;
    titleId?: string;
    titleHeadingLevel?: 1 | 2 | 3 | 4 | 5 | 6;
    text?: string;
    html?: string;
    role?: 'alert' | 'region' | 'status';
    disableAutoFocus?: boolean;
  }

  interface Props extends NotificationBannerProps {}

  let {
    type,
    titleText,
    titleHtml,
    titleId = 'public-good-notification-banner-title',
    titleHeadingLevel = 2,
    text,
    html,
    role,
    disableAutoFocus = false,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const successBanner = $derived(type === 'success');

  const bannerRole = $derived(role || (successBanner ? 'alert' : 'region'));

  const title = $derived(titleHtml || titleText || (successBanner ? 'Success' : 'Important'));

  const typeClasses = $derived((() => {
    const base = 'public-good-notification-banner alert';
    switch (type) {
      case 'success': return `${base} alert-success`;
      case 'warning': return `${base} alert-warning`;
      case 'error': return `${base} alert-error`;
      default: return `${base} alert-info`;
    }
  })());

  const bannerAttributes = $derived({
    ...attributes,
    ...restProps,
    role: bannerRole,
    'aria-labelledby': titleId,
    'data-disable-auto-focus': disableAutoFocus
  });

  let bannerElement: HTMLElement;

  $effect(() => {
    if (bannerElement && !disableAutoFocus && (type === 'success' || bannerRole === 'alert')) {
      bannerElement.focus();
    }
  });

  const HeadingTag = $derived(`h${titleHeadingLevel}` as keyof HTMLElementTagNameMap);
</script>

<div
  class="{typeClasses} {classes}"
  bind:this={bannerElement}
  tabindex="-1"
  {...bannerAttributes}
>
  <div class="flex">
    {#if type === 'success'}
      <svg class="w-6 h-6 flex-shrink-0 mr-3" fill="currentColor" viewBox="0 0 20 20" aria-hidden="true">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd" />
      </svg>
    {:else if type === 'warning'}
      <svg class="w-6 h-6 flex-shrink-0 mr-3" fill="currentColor" viewBox="0 0 20 20" aria-hidden="true">
        <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
      </svg>
    {:else if type === 'error'}
      <svg class="w-6 h-6 flex-shrink-0 mr-3" fill="currentColor" viewBox="0 0 20 20" aria-hidden="true">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.28 7.22a.75.75 0 00-1.06 1.06L8.94 10l-1.72 1.72a.75.75 0 101.06 1.06L10 11.06l1.72 1.72a.75.75 0 101.06-1.06L11.06 10l1.72-1.72a.75.75 0 00-1.06-1.06L10 8.94 8.28 7.22z" clip-rule="evenodd" />
      </svg>
    {:else}
      <svg class="w-6 h-6 flex-shrink-0 mr-3" fill="currentColor" viewBox="0 0 20 20" aria-hidden="true">
        <path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a.75.75 0 000 1.5h.253a.25.25 0 01.244.304l-.459 2.066A1.75 1.75 0 0010.747 15H11a.75.75 0 000-1.5h-.253a.25.25 0 01-.244-.304l.459-2.066A1.75 1.75 0 009.253 9H9z" clip-rule="evenodd" />
      </svg>
    {/if}

    <div class="flex-1">
      <div class="public-good-notification-banner__header">
        <svelte:element this={HeadingTag} class="public-good-notification-banner__title font-bold text-lg mb-2" id={titleId}>
          {#if titleHtml}
            {@html title}
          {:else}
            {title}
          {/if}
        </svelte:element>
      </div>

      <div class="public-good-notification-banner__content">
        {#if children}
          {@render children()}
        {:else if html}
          {@html html}
        {:else if text}
          <p class="public-good-notification-banner__heading m-0">
            {text}
          </p>
        {/if}
      </div>
    </div>
  </div>
</div>