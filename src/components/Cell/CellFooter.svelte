<script>
  export let primary = false;
  export let className;
  import classNames from "../../utils/classNames";
  let cls;
  $: cls = classNames({
    "weui-cell__ft": true,
    "weui-cell_primary": primary,
    [className]: className
  });
</script>

<div class={cls}>
  <slot />
</div>
