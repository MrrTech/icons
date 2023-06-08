<script lang="ts">
  import { onMount } from "svelte"
  import Tooltip from "bootstrap/js/dist/tooltip"

  import Navbar from "./components/Navbar.svelte"
  import Footer from "./components/Footer.svelte"

  import { icons } from "./data/icons"

  let search = ""

  $: filteredIcons = icons.map((icon) => ({
    icon,
    show: normalizeLabel(icon).toLowerCase().includes(search.toLowerCase()),
  }))

  let iconsContainer: HTMLElement
  onMount(() => {
    iconsContainer
      .querySelectorAll('[data-bs-toggle="tooltip"]')
      .forEach((el) => new Tooltip(el))
  })

  function normalizeLabel(icon: string): string {
    return icon
      .toLowerCase()
      .replace(/(_|-)/g, " ")
      .split(" ")
      .map((word) => word[0].toUpperCase() + word.slice(1))
      .join(" ")
  }

  let copied: number[] = []
  function copy(index: number, text: string): void {
    copied = [...copied, index]
    navigator.clipboard.writeText(text)
    setTimeout(() => {
      copied = copied.filter((idx) => idx !== index)
    }, 1500)
  }
</script>

<Navbar bind:search />

<main style="padding: 100px 0">
  <section class="container">
    <div class="d-flex flex-wrap" bind:this={iconsContainer}>
      {#each filteredIcons as { icon, show }, index (icon)}
        <div
          class="col-6 col-sm-4 col-md-3 col-lg-2 col-xl-1 p-2 {show
            ? ''
            : 'd-none'}"
        >
          <div
            class="card h-100"
            data-bs-toggle="tooltip"
            data-bs-title={normalizeLabel(icon)}
          >
            <div class="card-body h-100 p-2 text-center">
              <a
                target="_blank"
                href="{import.meta.env.BASE_URL}api/{icon}.svg"
              >
                <img
                  src="{import.meta.env.BASE_URL}api/{icon}.svg"
                  alt={icon}
                  style="max-width: 50px"
                  loading="lazy"
                />
              </a>

              <a
                class="icon-link icon-link-hover link-underline link-underline-opacity-0 mt-3"
                style="--bs-icon-link-transform: translate3d(0, -.125rem, 0);"
                href="#!"
                on:click|preventDefault={() =>
                  copy(
                    index,
                    window.location.origin +
                      import.meta.env.BASE_URL +
                      "api/" +
                      icon +
                      ".svg"
                  )}
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="16"
                  height="16"
                  fill="currentColor"
                  class="bi bi-clipboard"
                  viewBox="0 0 16 16"
                >
                  <path
                    d="M4 1.5H3a2 2 0 0 0-2 2V14a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V3.5a2 2 0 0 0-2-2h-1v1h1a1 1 0 0 1 1 1V14a1 1 0 0 1-1 1H3a1 1 0 0 1-1-1V3.5a1 1 0 0 1 1-1h1v-1z"
                  />
                  <path
                    d="M9.5 1a.5.5 0 0 1 .5.5v1a.5.5 0 0 1-.5.5h-3a.5.5 0 0 1-.5-.5v-1a.5.5 0 0 1 .5-.5h3zm-3-1A1.5 1.5 0 0 0 5 1.5v1A1.5 1.5 0 0 0 6.5 4h3A1.5 1.5 0 0 0 11 2.5v-1A1.5 1.5 0 0 0 9.5 0h-3z"
                  />
                </svg>
                {copied.includes(index) ? "Copied" : "Copy"}
              </a>
            </div>
          </div>
        </div>
      {/each}
    </div>
  </section>

  <Footer />
</main>
