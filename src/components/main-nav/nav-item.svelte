<script lang="ts">
  import { page } from "$app/stores";

  export let navItem: any;
  const { href, isHighlighted, label, isExternal } = navItem;
  const isPrefecthable = isExternal ? undefined : true;

  $: isActivePage =
    $page.path === "/" ? /\/$/.test(href) : href.indexOf($page.path) >= 0;
</script>

<style type="text/postcss">
  a {
    @media (min-width: 1050px) {
      @apply text-base;
    }
  }

  .active {
    color: var(--black);
  }
</style>

<a
  class:active={isActivePage && !isExternal}
  class:highlighted={isHighlighted}
  {href}
  on:click
  on:focus
  sveltekit:prefetch={isPrefecthable}
  class="text-black text-p-large sm:text-dark-grey sm:hover:text-black sm:focus:text-black"
>
  {label}
</a>
