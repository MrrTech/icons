<script lang="ts">
  import logo from "../assets/logo.png"
  import githubLogo from "../assets/github-logo.png"

  export let search: string
</script>

<nav class="navbar navbar-expand-lg fixed-top bg-primary">
  <div class="container-fluid">
    <span class="navbar-brand">
      <img src={logo} alt="logo" width="100px" />
    </span>

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
    </div>
  </div>
</nav>
