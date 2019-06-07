<script>
  export let access;
  export let href;
  export let link;
  export let htmlFor;
  export let className;
  import classNames from "../../utils/classNames";
  let cls = "";
  $: cls = classNames({
    "weui-cell": true,
    "weui-cell_access": access,
    "weui-cell_link": link,
    [className]: className
  });
</script>

{#if href}
  <a href={href} class={cls}>
    <slot />
  </a>
{:else if htmlFor}
  <label for={htmlFor} class={cls}>
    <slot />
  </label>
{:else}
  <div class={cls}>
    <slot />
  </div>
{/if}
