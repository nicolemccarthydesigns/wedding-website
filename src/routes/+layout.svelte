<script lang="ts">
  import "../app.css";

  const PASSWORD = "waterford2026";
  const SESSION_KEY = "wedding_auth";

  const isBrowser = typeof window !== "undefined";
  let unlocked = isBrowser
    ? sessionStorage.getItem(SESSION_KEY) === "true"
    : false;
  let input = "";
  let error = false;
  let shaking = false;

  function attempt() {
    if (input === PASSWORD) {
      sessionStorage.setItem(SESSION_KEY, "true");
      unlocked = true;
    } else {
      error = true;
      shaking = true;
      input = "";
      setTimeout(() => (shaking = false), 500);
    }
  }

  function handleKeydown(e: KeyboardEvent) {
    if (e.key === "Enter") attempt();
  }

  let scrollY = 0;
  let logoClass = "w-30";
  let mobileMenuOpen = false;

  $: logoClass = scrollY > 0 ? "w-20" : "w-30";
  $: opacity = scrollY > 0 ? 0.9 : 1;

  function toggleMenu() {
    mobileMenuOpen = !mobileMenuOpen;
  }

  function closeMenu() {
    mobileMenuOpen = false;
  }

  const navLinks = [
    { href: "#venue", label: "Venue" },
    { href: "#travel", label: "Travel" },
    { href: "#schedule", label: "Schedule" },
    { href: "#registry", label: "Registry" },
    { href: "#things-to-do", label: "Things To Do" },
    { href: "#faq", label: "FAQs" },
  ];
</script>

{#if !unlocked}
  <div
    class="fixed inset-0 z-[99999] bg-white flex flex-col items-center justify-center px-6"
  >
    <div class="flex flex-col items-center text-center max-w-sm w-full">
      <img
        src="/images/nav-logo-transparent.png"
        alt="Nicole & Dan"
        class="w-36 mb-8"
      />
      <!-- <p class="uppercase text-xs tracking-[0.12em] text-slate-400 mb-2">
        hello
      </p> -->
      <h2 class="!text-[42px] !pb-4">You're invited</h2>
      <p class="text-slate-500 text-base mb-8">
        Enter the password from your invitation to continue.
      </p>
      <div class="w-full" class:shake={shaking}>
        <input
          type="password"
          placeholder="Password"
          bind:value={input}
          on:keydown={handleKeydown}
          class="w-full border border-slate-200 rounded-md px-4 py-3 text-slate-900 text-sm focus:outline-none focus:border-slate-400 transition-colors placeholder:text-slate-300 mb-3"
        />
        {#if error}
          <p class="text-red-400 text-xs mb-3 text-left">
            Incorrect password. Please try again.
          </p>
        {/if}
        <button
          on:click={attempt}
          class="w-full bg-slate-900 text-white text-xs uppercase tracking-[0.08em] font-medium py-3 rounded-md hover:bg-slate-700 transition-colors"
        >
          Enter
        </button>
      </div>
    </div>
  </div>
{:else}
  <div class="bg-white text-slate-900">
    <nav class="w-full sticky top-0 z-[10000] bg-white/40 backdrop-blur-lg">
      <div
        class="max-w-[1200px] flex mx-auto h-14 items-center justify-between px-5 lg:px-6"
      >
        <a href="/" class="">
          <img
            src="/images/nav-logo-transparent.png"
            alt="Nicole & Dan"
            class="w-[115px]"
          />
        </a>

        <!-- Desktop menu -->
        <ul
          class="hidden items-center gap-7 text-[12px] font-medium uppercase tracking-[0.08em] text-slate-700 sm:flex"
        >
          {#each navLinks as link}
            <li>
              <a href={link.href} class="transition-colors hover:text-slate-900"
                >{link.label}</a
              >
            </li>
          {/each}
        </ul>

        <!-- Hamburger button (mobile only) -->
        <button
          class="sm:hidden flex flex-col justify-center items-center w-8 h-8 gap-[5px] focus:outline-none"
          aria-label="Toggle menu"
          aria-expanded={mobileMenuOpen}
          on:click={toggleMenu}
        >
          <span
            class="block h-[1.5px] w-5 bg-slate-700 transition-all duration-300 origin-center"
            class:rotate-45={mobileMenuOpen}
            class:translate-y-[6.5px]={mobileMenuOpen}
          ></span>
          <span
            class="block h-[1.5px] w-5 bg-slate-700 transition-all duration-300"
            class:opacity-0={mobileMenuOpen}
            class:scale-x-0={mobileMenuOpen}
          ></span>
          <span
            class="block h-[1.5px] w-5 bg-slate-700 transition-all duration-300 origin-center"
            class:-rotate-45={mobileMenuOpen}
            class:-translate-y-[6.5px]={mobileMenuOpen}
          ></span>
        </button>
      </div>

      <!-- Mobile dropdown menu -->
      <div
        class="sm:hidden overflow-hidden transition-all duration-300 ease-in-out"
        style="max-height: {mobileMenuOpen
          ? '400px'
          : '0px'}; opacity: {mobileMenuOpen ? '1' : '0'};"
      >
        <ul
          class="flex flex-col border-t border-slate-100 bg-white/80 backdrop-blur-lg px-5 pb-4 pt-3 text-[12px] font-medium uppercase tracking-[0.08em] text-slate-700"
        >
          {#each navLinks as link, i}
            <li
              class="transition-all duration-300"
              style="transition-delay: {mobileMenuOpen
                ? i * 40
                : 0}ms; transform: translateY({mobileMenuOpen
                ? '0'
                : '-8px'}); opacity: {mobileMenuOpen ? '1' : '0'};"
            >
              <a
                href={link.href}
                class="block py-3 transition-colors hover:text-slate-900 border-b border-slate-100 last:border-0"
                on:click={closeMenu}>{link.label}</a
              >
            </li>
          {/each}
        </ul>
      </div>
    </nav>

    <main class="mx-auto">
      <slot />
    </main>
    <footer
      class="z-10 flex h-16 w-full items-center justify-center border-t border-gray-100 bg-white mx-auto"
    >
      <div
        class="flex w-full max-w-[1280px] mx-auto px-4 py-4 text-xs text-gray-500 sm:px-8 md:px-20 items-center justify-center"
      >
        <p class="flex items-center gap-1">
          designed and developed with
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="currentColor"
            class="w-3 h-3 text-black"
          >
            <path
              d="M11.645 20.91l-.007-.003-.022-.012a15.247 15.247 0 01-.383-.218 25.18 25.18 0 01-4.244-3.17C4.688 15.36 2.25 12.174 2.25 8.25 2.25 5.322 4.714 3 7.688 3A5.5 5.5 0 0112 5.052 5.5 5.5 0 0116.313 3c2.973 0 5.437 2.322 5.437 5.25 0 3.925-2.438 7.111-4.739 9.256a25.175 25.175 0 01-4.244 3.17 15.247 15.247 0 01-.383.219l-.022.012-.007.004-.003.001a.752.752 0 01-.704 0l-.003-.001z"
            />
          </svg>
          by nicole
        </p>
      </div>
    </footer>
  </div>
{/if}

<style>
  @keyframes shake {
    0%,
    100% {
      transform: translateX(0);
    }
    20% {
      transform: translateX(-6px);
    }
    40% {
      transform: translateX(6px);
    }
    60% {
      transform: translateX(-4px);
    }
    80% {
      transform: translateX(4px);
    }
  }
  .shake {
    animation: shake 0.5s ease-in-out;
  }
</style>
