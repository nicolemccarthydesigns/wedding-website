<script lang="ts">
  export let label: string = "Button";
  export let href: string | undefined = undefined;
  export let target: string | undefined = undefined;
  export let size: "sm" | "md" | "lg" = "md";
  export let variant: "outline" | "solid" = "outline";
  export let type: "button" | "submit" | "reset" = "button";

  const sizeClasses = {
    sm: "px-2 py-2 text-sm",
    md: "px-4 py-2 text-base",
    lg: "px-10 py-4 text-lg",
  };
</script>

{#if href}
  <a {href} {target} rel={target === "_blank" ? "noopener noreferrer" : undefined} class="btn {sizeClasses[size]} {variant}" role="button">
    <slot>{label}</slot>
  </a>
{:else}
  <button {type} class="btn {sizeClasses[size]} {variant}" on:click>
    <slot>{label}</slot>
  </button>
{/if}

<style>
  .btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    border-radius: 6px;
    font-family: inherit;
    font-weight: 400;
    letter-spacing: 0.01em;
    cursor: pointer;
    transition:
      background-color 150ms ease,
      border-color 150ms ease,
      color 150ms ease,
      box-shadow 150ms ease;
    text-decoration: none;
    white-space: nowrap;
    user-select: none;
  }

  .outline {
    background-color: #ffffff;
    border: 1px solid #e2e8f0;
    color: #1e293b;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.04);
  }

  .outline:hover {
    background-color: #f8fafc;
    border-color: #94a3b8;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.08);
  }

  .outline:active {
    background-color: #f1f5f9;
    box-shadow: none;
  }

  .solid {
    background-color: #0f172a;
    color: #ffffff;
    box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  }

  .solid:hover {
    background-color: #1e293b;

    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
  }

  .solid:active {
    background-color: #0f172a;
    box-shadow: none;
  }

  .btn:focus-visible {
    outline: 2px solid #94a3b8;
    outline-offset: 2px;
  }
</style>
