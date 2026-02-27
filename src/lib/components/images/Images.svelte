<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface ImagesProps extends BaseComponentProps {
    src: string;
    alt: string;
    caption?: string;
    sizes?: string;
    srcset?: string;
  }

  interface Props extends ImagesProps {}

  let {
    src,
    alt,
    caption,
    sizes,
    srcset,
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const figureAttributes = $derived({
    ...attributes,
    ...restProps
  });
</script>

<figure
  class="public-good-image {classes}"
  {...figureAttributes}
>
  <img
    class="public-good-image__img w-full h-auto rounded-lg shadow-sm"
    {src}
    {alt}
    {sizes}
    {srcset}
    loading="lazy"
  />

  {#if caption}
    <figcaption class="public-good-image__caption text-sm text-base-content/70 mt-2 italic">
      {caption}
    </figcaption>
  {/if}

  {#if children}
    {@render children()}
  {/if}
</figure>