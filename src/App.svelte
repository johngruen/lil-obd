<script>
  import { onboarded } from "./stores.js";
  import { fade, fly } from "svelte/transition";
  let panel = 0;
  let loaded = false;

  const load = num => {
    setTimeout(() => {
      loaded = true;
    }, num);
  };

  const increment = () => {
    panel++;
  };

  const restart = () => {
    panel = 0;
    loaded = false;
    load(1000);
  };

  load(10);
</script>

<style>
  main {
    min-height: 100vh;
    position: relative;
  }
  .logo {
    background: url("chrome://branding/content/about-logo.svg") top center/112px
      no-repeat;
    flex: 0 0 112px;
    width: 100%;
    margin-bottom: 24px;
  }

  .zap {
    position: relative;
  }

  .zap:after {
    background-image: url("chrome://activity-stream/content/data/content/assets/short-zap.svg");
    display: block;
    background-repeat: no-repeat;
    background-size: 100% 100%;
    content: "";
    position: absolute;
    top: calc(100% - 0.15em);
    width: 100%;
    height: 0.3em;
    left: 0;
    z-index: -1;
  }
  .panel {
    display: flex;
    min-height: 100vh;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding: 60px 60px 120px;
    position: relative;
    z-index: 1;
  }

  h1 {
    font-size: 48px;
    line-height: 56px;
    font-weight: bold;
    margin: 0 6px;
    color: var(--welcome-header-text-color-1);
    text-shadow: 0 0 20px rgba(255, 255, 255, 0.1);
    max-width: 600px;
    text-align: center;
  }

  h2 {
    font-size: 20px;
    font-weight: normal;
    margin: 16px 6px 0;
    color: var(--grey-subtitle-1);
    line-height: 28px;
    max-width: 750px;
    letter-spacing: -0.01em;
  }

  button {
    font-size: 20px;
    margin: 36px 0 0;
    padding: 16px 32px;
    white-space: nowrap;
    background-color: var(--newtab-button-primary-color);
    color: var(--welcome-button-text-color);
    fill: currentColor;
    position: relative;
    font-family: inherit;
    cursor: pointer;
    border: 0;
    border-radius: 8px;
    box-shadow: -4px -4px 18px rgba(255, 255, 255, 0.2),
      4px 4px 18px rgba(12, 12, 13, 0.1);
  }

  .bg {
    position: fixed;
    z-index: 0;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background: url("/images/shapes-2.svg") no-repeat;
    background-position: left 0 bottom 0;
    opacity: 0.2;
    background-size: cover;
  }

  .p {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .logo {
    position: relative;
    transition: top 100ms;
  }

  a {
    color: var(--newtab-button-primary-color);
  }

  .box {
    background: #fff;
    border-radius: 16px;
    height: 160px;
    width: 400px;
    margin-top: 32px;
    box-shadow: -4px -4px 18px rgba(255, 255, 255, 0.2),
      4px 4px 18px rgba(12, 12, 13, 0.1);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .sign {
    position: absolute;
    top: 16px;
    right: 16px;
  }

  .p a {
    display: block;
    margin-top: 12px;
  }
</style>

<main>
  {#if loaded}
    <div class="panel" transition:fade={{ duration: 500, delay: 500 }}>
      {#if panel === 0}
        <div class="sign" out:fly={{ duration: 250, y: -40 }}>
          Have an account?
          <a href="">Sign in</a>
        </div>
      {/if}
      {#if panel === 0}
        <div class="logo" />
        <div class="p">
          <h1>
            Welcome to
            <span class="zap">Firefox</span>
          </h1>
          <h2>
            The fast, safe, and private browser that’s backed by a non-profit.
          </h2>
          <button on:click={increment}>Start Setup</button>
        </div>
      {:else if panel === 1}
        <div class="p" in:fly={{ duration: 500, delay: 250, x: 100 }}>
          <h1>
            Import your passwords, bookmarks, and
            <span class="zap">more</span>
          </h1>
          <h2>
            Coming from another browser? It’s easy to bring everything to
            Nightly.
          </h2>
          <div class="box" in:fly={{ duration: 500, delay: 250, x: 100 }}>
            Widget
          </div>
          <button on:click={increment}>Start Import</button>
          <a href="" on:click={increment}>Skip</a>
        </div>
      {:else if panel === 2}
        <div class="p" in:fly={{ duration: 500, delay: 250, x: 100 }}>
          <h1>
            Choose a
            <span class="zap">look</span>
          </h1>
          <h2>Personalize Nightly with a theme.</h2>
          <div class="box" in:fly={{ duration: 500, delay: 250, x: 100 }}>
            Widget
          </div>
          <button on:click={increment}>Save Theme</button>

          <a href="" on:click={increment}>Skip</a>
        </div>
      {:else if panel === 3}
        <div class="p" in:fly={{ duration: 500, delay: 250, x: 100 }}>
          <h1>
            Demo
            <span class="zap">Over</span>
            !
          </h1>
          <button on:click={restart}>Restart</button>
        </div>
      {/if}
    </div>
    <div class="bg" transition:fade={{ duration: 500 }} />
  {/if}
</main>
