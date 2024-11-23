<script>
  import "../app.css";
  import {
    AlignHorizontalJustifyCenter,
    Maximize,
    Minus,
    X,
  } from "lucide-svelte";
  import { getCurrentWindow } from "@tauri-apps/api/window";

  const currentWindow = getCurrentWindow();

  const minimize = () => {
    currentWindow.minimize();
  };

  const maximize = async () => {
    if (await currentWindow.isMaximized()) {
      currentWindow.unmaximize();
    } else {
      currentWindow.maximize();
    }
  };

  const close = () => {
    currentWindow.close();
  };

  let { children } = $props();
</script>

<header class="bg-zinc-800 h-12 select-none bg-fixed">
  <nav
    data-tauri-drag-region
    class="mx-auto flex items-center justify-between"
    aria-label="Global"
  >
    <div class="mx-1 p-3">
      <AlignHorizontalJustifyCenter class="square-4" />
    </div>
    <ul class="flex gap-x-1">
      <li>
        <button onclick={minimize} class="window-control-button">
          <Minus size="16" />
        </button>
      </li>
      <li>
        <button onclick={maximize} class="window-control-button">
          <Maximize size="16" />
        </button>
      </li>
      <li>
        <button onclick={close} class="window-control-button">
          <X size="16" />
        </button>
      </li>
    </ul>
  </nav>
</header>

<div class="bg-zinc-900 h-[1px]"></div>

<main class="bg-zinc-800 h-screen">
  {@render children?.()}
</main>

<style lang="postcss">
  :global(body) {
    overflow: hidden;
    user-select: none;
    color: white;
  }

  .window-control-button {
    @apply hover:bg-zinc-600 p-4;
  }
</style>
