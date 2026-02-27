<script lang="ts">
  import type { ButtonProps } from '$lib/types.js';

  interface Props extends ButtonProps {}

  let {
    element = 'button',
    text,
    html,
    name,
    type = 'submit',
    value,
    disabled = false,
    href,
    variant = 'primary',
    preventDoubleClick = false,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  const elementType = $derived(element || (href ? 'a' : 'button'));

  const variantClasses = $derived(
    variant === 'secondary' ? 'btn-secondary' :
    variant === 'warning' ? 'btn-warning' :
    variant === 'reverse' ? 'btn-outline btn-primary' :
    variant === 'login' ? 'btn-primary btn-wide' :
    'btn-primary'
  );

  const elementAttributes = $derived({
    ...attributes,
    ...restProps,
    ...(preventDoubleClick && elementType !== 'a' ? { 'data-prevent-double-click': 'true' } : {}),
    ...(disabled && elementType !== 'a' ? { disabled: true, 'aria-disabled': 'true' } : {})
  });
</script>

{#if elementType === 'a'}
  <a
    class="btn {variantClasses} {disabled ? 'btn-disabled' : ''} {classes}"
    href={href || '#'}
    role="button"
    draggable="false"
    tabindex={disabled ? -1 : 0}
    aria-disabled={disabled ? 'true' : undefined}
    {...elementAttributes}
  >
    {#if html}
      {@html html}
    {:else}
      {text}
    {/if}
  </a>
{:else if elementType === 'input'}
  <input
    class="btn {variantClasses} {classes}"
    {value}
    {name}
    {type}
    {disabled}
    {...elementAttributes}
  />
{:else}
  <button
    class="btn {variantClasses} {classes}"
    {name}
    {type}
    {value}
    {disabled}
    {...elementAttributes}
  >
    {#if html}
      {@html html}
    {:else}
      {text}
    {/if}
  </button>
{/if}