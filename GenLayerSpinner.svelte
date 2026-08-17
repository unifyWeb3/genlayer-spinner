<script lang="ts">
  import './spinner.css';

  export let size = 20;
  export let label: string | null = null;

  let className = '';
  export { className as class };

  $: style = `--gl-spinner-size: ${size}px;`;
</script>

<span
  class={`gl-spinner ${className}`.trim()}
  {style}
  role={label ? 'status' : undefined}
  aria-hidden={label ? undefined : 'true'}
>
  <svg
    class="gl-spinner__svg"
    viewBox="0 0 100 100"
    preserveAspectRatio="xMidYMid meet"
    aria-hidden="true"
    focusable="false"
  >
    <g transform="translate(5 7.7) scale(.92)">
      <g class="gl-spinner__facet gl-spinner__facet--left" data-facet="left">
        <polygon points="44.26 32.35 27.72 67.12 43.29 74.9 0 91.93 44.26 0 44.26 32.35" />
      </g>
      <g class="gl-spinner__facet gl-spinner__facet--right" data-facet="right">
        <polygon points="53.5 32.35 70.04 67.12 54.47 74.9 97.76 91.93 53.5 0 53.5 32.35" />
      </g>
      <g class="gl-spinner__facet gl-spinner__facet--core" data-facet="core">
        <polygon points="48.64 43.78 58.33 62.94 48.64 67.69 39.47 62.92 48.64 43.78" />
      </g>
    </g>
  </svg>

  {#if label}
    <span class="gl-spinner__sr-only">{label}</span>
  {/if}
</span>
