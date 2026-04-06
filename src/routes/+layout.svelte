<script>
  export let data;
</script>

<div class="min-h-screen bg-gradient-to-b from-white via-slate-50 to-slate-100 text-slate-900">
  <header class="border-b border-slate-200 bg-white/80 backdrop-blur-md">
    <div class="mx-auto flex max-w-6xl items-center justify-between px-6 py-6">
      <div>
        <p class="text-sm uppercase tracking-[0.3em] text-slate-500">Nicole &amp; Matt</p>
        <h1 class="mt-2 text-3xl font-semibold tracking-tight text-slate-900 sm:text-4xl">Wedding Website</h1>
      </div>
      <nav class="hidden space-x-6 text-sm font-medium text-slate-600 md:flex">
        <a href="#details" class="hover:text-slate-900">Details</a>
        <a href="#schedule" class="hover:text-slate-900">Schedule</a>
        <a href="#travel" class="hover:text-slate-900">Travel</a>
      </nav>
    </div>
  </header>

  <main class="mx-auto max-w-6xl px-6 py-10">
    <slot />
  </main>
</div>
