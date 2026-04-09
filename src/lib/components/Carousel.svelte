<script lang="ts">
  import { onDestroy, onMount } from "svelte";

  export let images: { src: string; alt: string }[] = [];

  const DWELL_MS = 4000;
  const TRANSITION_MS = 500;

  let current = 0;
  let previous: number | null = null;
  let transitioning = false;
  let autoplayTimer: ReturnType<typeof setTimeout> | null = null;

  function crossfadeTo(index: number) {
    if (transitioning || index === current) return;
    previous = current;
    current = index;
    transitioning = true;
    setTimeout(() => {
      previous = null;
      transitioning = false;
    }, TRANSITION_MS);
  }

  function advance(dir: "left" | "right") {
    const next =
      dir === "right"
        ? (current + 1) % images.length
        : (current - 1 + images.length) % images.length;
    crossfadeTo(next);
  }

  function goTo(index: number) {
    crossfadeTo(index);
  }

  function scheduleNext() {
    autoplayTimer = setTimeout(() => {
      previous = current;
      current = (current + 1) % images.length;
      transitioning = true;
      // Store the cleanup timer in autoplayTimer so stopAutoplay() can cancel it too
      autoplayTimer = setTimeout(() => {
        previous = null;
        transitioning = false;
        scheduleNext();
      }, TRANSITION_MS);
    }, DWELL_MS);
  }

  function startAutoplay() {
    stopAutoplay();
    scheduleNext();
  }

  function stopAutoplay() {
    if (autoplayTimer !== null) {
      clearTimeout(autoplayTimer);
      autoplayTimer = null;
    }
    // If a transition was mid-flight, snap it to completion so
    // transitioning never gets stuck as true
    if (transitioning) {
      previous = null;
      transitioning = false;
    }
  }

  onMount(() => startAutoplay());
  onDestroy(() => stopAutoplay());
</script>

<div
  class="carousel"
  role="region"
  aria-label="Image gallery"
  on:mouseenter={stopAutoplay}
  on:mouseleave={startAutoplay}
>
  <div class="track">
    {#each images as image, i}
      <img
        src={image.src}
        alt={image.alt}
        class="slide"
        class:active={i === current}
        class:exiting={i === previous}
        aria-hidden={i !== current && i !== previous}
      />
    {/each}
  </div>

  <button
    class="chevron chevron-left"
    on:click={() => { stopAutoplay(); advance("left"); startAutoplay(); }}
    aria-label="Previous image"
  >
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <polyline points="15 18 9 12 15 6" />
    </svg>
  </button>

  <button
    class="chevron chevron-right"
    on:click={() => { stopAutoplay(); advance("right"); startAutoplay(); }}
    aria-label="Next image"
  >
    <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
      <polyline points="9 18 15 12 9 6" />
    </svg>
  </button>

  <div class="dots" role="tablist">
    {#each images as _, i}
      <button
        role="tab"
        aria-selected={i === current}
        aria-label={`Go to image ${i + 1}`}
        class="dot"
        class:dot-active={i === current}
        on:click={() => { stopAutoplay(); goTo(i); startAutoplay(); }}
      />
    {/each}
  </div>
</div>

<style>
  .carousel {
    position: relative;
    width: 100%;
    max-width: 1200px;
    margin-top: 2.5rem;
    border-radius: 6px;
    overflow: hidden;
  }

  .track {
    position: relative;
    width: 100%;
    aspect-ratio: 16 / 9;
    background: #0f172a;
    isolation: isolate;
  }

  .slide {
    position: absolute;
    inset: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0;
    transition: opacity 500ms ease;
    will-change: opacity;
    pointer-events: none;
  }

  .slide.active {
    opacity: 1;
    pointer-events: auto;
  }

  .slide.exiting {
    opacity: 0;
  }

  /* Chevron buttons */
  .chevron {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    border-radius: 6px;
    background-color: rgba(15, 23, 42, 0.65);
    color: #ffffff;
    border: none;
    cursor: pointer;
    opacity: 0;
    transition: background-color 150ms ease, opacity 150ms ease, box-shadow 150ms ease;
    z-index: 10;
  }

  .carousel:hover .chevron {
    opacity: 1;
  }

  .chevron:hover {
    background-color: #0f172a;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
  }

  .chevron:active {
    background-color: #1e293b;
    box-shadow: none;
  }

  .chevron:focus-visible {
    outline: 2px solid #94a3b8;
    outline-offset: 2px;
    opacity: 1;
  }

  .chevron-left {
    left: 12px;
  }

  .chevron-right {
    right: 12px;
  }

  /* Dot indicators */
  .dots {
    position: absolute;
    bottom: 12px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 6px;
    z-index: 10;
  }

  .dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.45);
    border: none;
    cursor: pointer;
    padding: 0;
    transition: background-color 200ms ease, transform 200ms ease;
  }

  .dot.dot-active {
    background-color: #ffffff;
    transform: scale(1.3);
  }

  .dot:focus-visible {
    outline: 2px solid #94a3b8;
    outline-offset: 2px;
  }
</style>
