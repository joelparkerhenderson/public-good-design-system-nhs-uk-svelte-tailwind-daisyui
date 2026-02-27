<script lang="ts">
  import type { BaseComponentProps } from '$lib/types.js';

  interface TagProps extends BaseComponentProps {
    text?: string;
    html?: string;
    variant?: 'white' | 'grey' | 'green' | 'aqua-green' | 'blue' | 'purple' | 'pink' | 'red' | 'orange' | 'yellow';
  }

  interface Props extends TagProps {}

  let {
    text = '',
    html,
    variant = 'grey',
    classes = '',
    attributes = {},
    children,
    ...restProps
  }: Props = $props();

  const tagAttributes = $derived({
    ...attributes,
    ...restProps
  });

  const variantMap: Record<string, string> = {
    'white': 'badge-ghost',
    'grey': 'badge-neutral',
    'green': 'badge-success',
    'aqua-green': 'badge-info',
    'blue': 'badge-primary',
    'purple': 'badge-secondary',
    'pink': 'bg-pink-100 text-pink-800 border-pink-200',
    'red': 'badge-error',
    'orange': 'badge-warning',
    'yellow': 'bg-yellow-100 text-yellow-800 border-yellow-200'
  };

  const variantClasses = $derived(variantMap[variant] || variantMap.grey);
</script>

<span
  class="public-good-tag badge badge-outline {variantClasses} {classes}"
  {...tagAttributes}
>
  {#if children}
    {@render children()}
  {:else if html}
    {@html html}
  {:else}
    {text}
  {/if}
</span>

<style>
  .public-good-tag {
    font-weight: 600;
    font-size: 0.875rem;
    line-height: 1.2;
    text-transform: none;
    white-space: nowrap;
    vertical-align: middle;
  }

  .public-good-tag.bg-pink-100 {
    background-color: #fce7f3;
    color: #9d174d;
    border-color: #fbcfe8;
  }

  .public-good-tag.bg-yellow-100 {
    background-color: #fef3c7;
    color: #92400e;
    border-color: #fde68a;
  }
</style>