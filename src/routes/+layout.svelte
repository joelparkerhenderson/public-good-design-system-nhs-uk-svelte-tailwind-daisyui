<script lang="ts">
  import '../app.css';

  let { children } = $props();
</script>

<main class="min-h-screen bg-base-100">
  {@render children()}
</main>