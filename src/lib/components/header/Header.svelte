<script lang="ts">
  import type { HeaderProps } from '$lib/types';

  interface Props extends HeaderProps {}

  let {
    serviceName = '',
    serviceUrl = '/',
    showNavigation = false,
    navigationItems = [],
    showSearch = false,
    searchAction = '/search',
    searchPlaceholder = 'Search',
    logoText = 'Public Good Design System',
    logoUrl = '/',
    organisational = false,
    transactional = false,
    children,
    classes = '',
    attributes = {},
    ...restProps
  }: Props = $props();

  let mobileMenuOpen = $state(false);

  function toggleMobileMenu() {
    mobileMenuOpen = !mobileMenuOpen;
  }

  const headerAttributes = $derived({
    ...attributes,
    ...restProps
  });

  const headerVariantClass = $derived(
    transactional ? 'public-good-header--transactional' :
    organisational ? 'public-good-header--organisational' :
    ''
  );
</script>

<header
  class="public-good-header bg-primary text-primary-content {headerVariantClass} {classes}"
  {...headerAttributes}
>
  <div class="public-good-header__container container mx-auto px-4">
    <div class="public-good-header__content flex items-center justify-between py-4">

      <!-- Logo Section -->
      <div class="public-good-header__logo flex items-center">
        <a
          class="public-good-header__logo-link text-primary-content hover:text-primary-content/80 text-xl font-bold no-underline"
          href={logoUrl}
          aria-label="{logoText} homepage"
        >
          <div class="flex items-center gap-3">
            <div class="w-8 h-8 bg-primary-content rounded-sm flex items-center justify-center">
              <span class="text-primary font-bold text-sm">PG</span>
            </div>
            <span class="hidden sm:inline">{logoText}</span>
          </div>
        </a>
      </div>

      <!-- Service Name Section -->
      {#if serviceName}
        <div class="public-good-header__service-name flex-1 mx-6">
          <a
            class="public-good-header__service-name-link text-primary-content hover:text-primary-content/80 text-lg font-semibold no-underline"
            href={serviceUrl}
          >
            {serviceName}
          </a>
        </div>
      {/if}

      <!-- Search Section -->
      {#if showSearch && !transactional}
        <div class="public-good-header__search hidden md:block">
          <form
            class="public-good-header__search-form flex items-center gap-2"
            role="search"
            action={searchAction}
            method="get"
          >
            <label class="sr-only" for="public-good-search-field">Search</label>
            <input
              class="input input-sm w-48 bg-base-100 text-base-content"
              id="public-good-search-field"
              name="q"
              type="search"
              placeholder={searchPlaceholder}
              autocomplete="off"
            />
            <button
              class="btn btn-sm btn-secondary"
              type="submit"
              aria-label="Search"
            >
              <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
              </svg>
            </button>
          </form>
        </div>
      {/if}

      <!-- Mobile Menu Toggle -->
      {#if showNavigation && navigationItems.length > 0}
        <div class="public-good-header__mobile-toggle md:hidden">
          <button
            class="btn btn-ghost btn-sm text-primary-content"
            onclick={toggleMobileMenu}
            aria-expanded={mobileMenuOpen}
            aria-controls="public-good-mobile-navigation"
            aria-label="Toggle navigation menu"
          >
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>
        </div>
      {/if}
    </div>
  </div>

  <!-- Navigation Section -->
  {#if showNavigation && navigationItems.length > 0 && !transactional}
    <div class="public-good-navigation-container bg-primary-focus">
      <div class="container mx-auto px-4">
        <!-- Desktop Navigation -->
        <nav
          class="public-good-navigation hidden md:block"
          aria-label="Primary navigation"
        >
          <ul class="public-good-header__navigation-list flex items-center">
            {#each navigationItems as item}
              <li class="public-good-header__navigation-item">
                <a
                  class="public-good-header__navigation-link block px-4 py-3 text-primary-content hover:text-primary-content/80 hover:bg-primary/20 no-underline transition-colors"
                  href={item.href}
                  {...(item.attributes || {})}
                >
                  {#if item.html}
                    {@html item.html}
                  {:else}
                    {item.text}
                  {/if}
                </a>
              </li>
            {/each}
          </ul>
        </nav>

        <!-- Mobile Navigation -->
        <nav
          class="public-good-navigation md:hidden {mobileMenuOpen ? 'block' : 'hidden'}"
          id="public-good-mobile-navigation"
          aria-label="Primary navigation (mobile)"
        >
          <ul class="public-good-header__navigation-list">
            {#each navigationItems as item}
              <li class="public-good-header__navigation-item border-b border-primary/20 last:border-b-0">
                <a
                  class="public-good-header__navigation-link block px-4 py-4 text-primary-content hover:text-primary-content/80 hover:bg-primary/20 no-underline transition-colors"
                  href={item.href}
                  {...(item.attributes || {})}
                >
                  {#if item.html}
                    {@html item.html}
                  {:else}
                    {item.text}
                  {/if}
                </a>
              </li>
            {/each}
          </ul>
        </nav>
      </div>
    </div>
  {/if}

  {#if children}
    <div class="public-good-header__custom-content">
      {@render children()}
    </div>
  {/if}
</header>