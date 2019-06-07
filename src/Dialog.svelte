<script>
    import { createEventDispatcher } from 'svelte';
    import { fade } from 'svelte/transition';
    const dispatcher = createEventDispatcher();
    export let isShow = false;
    export let type = 'ios';
    export let isMaskCancel = true;
    export let title;
    export let content;
    export let mainButton = {
      text: '主操作',
      onClick: () => {
        handleClose({
          isShow: false,
          value: 1
        });
      }
    }
    export let subButton;

    const handleMaskClose = () => {
        if (!isMaskCancel) return;
        handleClose({
          isShow: false
        });
    }

    const handleMainButtonClick = () => {
      handleClose({
        isShow: false,
        value: 1
      });
    }

    const handleSubButtonClick = () => {
      handleClose({
        isShow: false,
        value: 0
      });
    }

    const handleClose = (value) => {
        dispatcher('cancel', value);
    }

    const handleMoveTouch = (e) => {
      e.preventDefault();
    }
</script>

<style>
    /* .weui-dialog_transition {
        transition: opacity .2s linear 0s;
    } */
</style>

<!-- <div class={type === 'android' ? 'weui-skin_android weui-dialog_transition' : 'weui-dialog_transition'}>
  <div class="weui-mask" style={isShow ? 'opacity: 1;' : 'opacity: 0;'}></div>
  <div class={type === 'android' ? 'weui-dialog weui-skin_android' : 'weui-dialog'} style={isShow ? 'opacity: 1' : 'opacity: 0;'}>
      <div class="weui-dialog__hd"><strong class="weui-dialog__title">{title}</strong></div>
      <div class="weui-dialog__bd">{content}</div>
      <div class="weui-dialog__ft">
          <a href="javascript:;" class="weui-dialog__btn weui-dialog__btn_default" on:click={handleSubButtonClick}>{mainButton.text}</a>
          <a href="javascript:;" class="weui-dialog__btn weui-dialog__btn_primary" on:click={handleMainButtonClick}>{subButton.text}</a>
      </div>
  </div>
</div> -->
{#if isShow}
<div in:fade={{ duration: 200 }}>
  <div class="weui-mask" on:click={handleMaskClose} on:movetouch={handleMoveTouch}></div>
  <div class={type === 'android' ? 'weui-dialog weui-skin_android' : 'weui-dialog'}>
      {#if title}
      <div class="weui-dialog__hd"><strong class="weui-dialog__title">{title}</strong></div>
      {/if}
      <div class="weui-dialog__bd">{content}</div>
      <div class="weui-dialog__ft">
          {#if subButton}
          <a href="javascript:;" class="weui-dialog__btn weui-dialog__btn_default" on:click={handleMainButtonClick}>{subButton.text}</a>
          {/if}
          <a href="javascript:;" class="weui-dialog__btn weui-dialog__btn_primary" on:click={handleSubButtonClick}>{mainButton.text}</a>
      </div>
  </div>
</div>
{/if}
