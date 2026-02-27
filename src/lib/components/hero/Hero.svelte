<script lang="ts">
  import type { HeroProps } from '$lib/types';

  interface Props extends HeroProps {}

  let {
    heading = '',
    headingHtml = '',
    headingLevel = 1,
    text = '',
    html = '',
    backgroundImage = '',
    overlay = true,
    overlayOpacity = 60,
    variant = 'default',
    actions = [],
    minHeight = 'min-h-96',
    textAlign = 'center',
    children,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const HeadingTag = $derived(`h${headingLevel}` as keyof HTMLElementTagNameMap);

  const heroAttributes = $derived({
    ...attributes,
    ...restProps
  });

  const heroVariantClass = $derived(
    variant === 'emergency' ? 'bg-error text-error-content' :
    variant === 'urgent' ? 'bg-warning text-warning-content' :
    variant === 'success' ? 'bg-success text-success-content' :
    variant === 'info' ? 'bg-info text-info-content' :
    'bg-primary text-primary-content'
  );

  const textAlignClass = $derived(
    textAlign === 'left' ? 'text-left' :
    textAlign === 'right' ? 'text-right' :
    'text-center'
  );
</script>

<section
  class="public-good-hero hero {minHeight} {heroVariantClass} {classes}"
  style={backgroundImage ? `background-image: url('${backgroundImage}')` : ''}
  {...heroAttributes}
>
  {#if backgroundImage && overlay}
    <div class="hero-overlay bg-neutral" style="opacity: {overlayOpacity / 100}"></div>
  {/if}

  <div class="hero-content {textAlignClass}">
    <div class="public-good-hero__content max-w-4xl">
      {#if children}
        {@render children()}
      {:else}
        {#if heading || headingHtml}
          <svelte:element this={HeadingTag} class="public-good-hero__heading mb-5 text-4xl md:text-5xl font-bold">
            {#if headingHtml}
              {@html headingHtml}
            {:else}
              {heading}
            {/if}
          </svelte:element>
        {/if}

        {#if text || html}
          <div class="public-good-hero__text mb-5 text-lg md:text-xl">
            {#if html}
              {@html html}
            {:else}
              <p>{text}</p>
            {/if}
          </div>
        {/if}

        {#if actions.length > 0}
          <div class="public-good-hero__actions flex flex-col sm:flex-row gap-4 justify-center">
            {#each actions as action}
              <a
                class="btn {action.variant === 'secondary' ? 'btn-secondary' : action.variant === 'outline' ? 'btn-outline' : 'btn-primary'} btn-lg"
                href={action.href}
                {...(action.attributes || {})}
              >
                {#if action.html}
                  {@html action.html}
                {:else}
                  {action.text}
                {/if}
              </a>
            {/each}
          </div>
        {/if}
      {/if}
    </div>
  </div>
</section>