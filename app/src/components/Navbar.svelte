<script lang="ts">
  import logo from "../assets/logo.png"
  import githubLogo from "../assets/github-logo.png"

  export let search: string
</script>

<nav class="navbar navbar-expand-lg fixed-top bg-primary">
  <div class="container-fluid">
    <a
      class="navbar-brand"
      href="https://mrrtech.github.io/profile/"
      target="_blank"
    >
      <img src={logo} alt="logo" width="100px" />
    </a>

    <form role="search" on:submit|preventDefault>
      <input
        class="form-control"
        type="search"
        placeholder="Search for icons"
        aria-label="Search"
        bind:value={search}
      />
    </form>

    <div>
      <a target="_blank" href="https://github.com/MrrTech/icons">
        <img
          src={githubLogo}
          alt="github-logo"
          width="30px"
          style="cursor: pointer"
        />
      </a>
      <a
        class="btn btn-dark ms-1"
        target="_blank"
        href="{import.meta.env.BASE_URL}api.json"
      >
        api.json
      </a>
    </div>
  </div>
</nav>
