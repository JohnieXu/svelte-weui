<script>
  import { createEventDispatcher } from 'svelte'
  import { fade } from 'svelte/transition'
  const dispatcher = createEventDispatcher()
  export let isShow = false
  export let title = '弹窗标题'
  export let content = '弹窗内容，告知当前页面信息等'
  export let isMaskCancel = false

  const handleClick = (isMaskCancel) => {
    if (isMaskCancel) return
    isShow = false
    dispatcher('ok', { isShow })
  }
  
  const handleMoveTouch = (e) => {
    e.preventDefault();
  }

</script>

{#if isShow}
<div in:fade={{ duration: 200 }}>
  <div class="weui-mask" on:click={() => { handleClick(!isMaskCancel) }} on:movetouch={handleMoveTouch} />
  <div class="weui-dialog">
    <div class="weui-dialog__hd">
      <strong class="weui-dialog__title">{title}</strong>
    </div>
    <div class="weui-dialog__bd">{content}</div>
    <div class="weui-dialog__ft">
      <a href="javascript:;" on:click={() => { handleClick(isMaskCancel) } } class="weui-dialog__btn weui-dialog__btn_primary">
        确定
      </a>
    </div>
  </div>
</div>
{/if}
