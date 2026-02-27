<script lang="ts">
  import type { FooterProps } from '$lib/types';

  interface Props extends FooterProps {}

  let {
    links = [],
    copyright = '© NHS England',
    visuallyHiddenText = 'Support links',
    children,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const footerAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<footer
  class="public-good-footer bg-base-200 border-t border-base-300 py-8 mt-auto {classes}"
  {...footerAttributes}
>
  <div class="container mx-auto px-4 max-w-6xl">
    <h2 class="sr-only">{visuallyHiddenText}</h2>

    <div class="public-good-footer__content">
      {#if children}
        {@render children()}
      {:else if links.length > 0}
        <nav class="public-good-footer__nav mb-6">
          <ul class="public-good-footer__list flex flex-wrap gap-x-6 gap-y-2 justify-center sm:justify-start">
            {#each links as link}
              <li class="public-good-footer__list-item">
                <a
                  class="public-good-footer__list-item-link link link-hover text-base-content/70 hover:text-primary text-sm"
                  href={link.href}
                  {...(link.attributes || {})}
                >
                  {#if link.html}
                    {@html link.html}
                  {:else}
                    {link.text}
                  {/if}
                </a>
              </li>
            {/each}
          </ul>
        </nav>
      {/if}

      {#if copyright}
        <div class="public-good-footer__copyright">
          <p class="text-center sm:text-left text-sm text-base-content/60 m-0">
            {copyright}
          </p>
        </div>
      {/if}
    </div>
  </div>
</footer>