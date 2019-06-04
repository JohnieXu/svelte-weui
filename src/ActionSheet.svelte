<script>
    import { createEventDispatcher } from 'svelte';
    import { fade } from 'svelte/transition';
    const dispatcher = createEventDispatcher();
    export let isShow = false;
    export let type = 'ios';
    export let isMaskCancel = true;
    export let title;
    export let menu = [];

    const handleMaskClose = () => {
        if (isMaskCancel) {
            dispatcher('cancel')
        }
    }

    const handleMenuItemClick = (value) => {
        console.log(value);
        handleClose(value);
    }

    const handleClose = (value) => {
        dispatcher('cancel', value);
    }

    const handleMoveTouch = (e) => {
        e.preventDefault();
    }
</script>

<style>
    .weui-mask_transition {
        transition: opacity .2s linear 0s;
    }
</style>

<div class={type === 'android' ? 'weui-skin_android weui-mask_transition' : ''}>
    <div class="weui-mask weui-mask_transition" style={isShow ? "opacity: 1;" : "opacity: 0; display: none;"} on:click={handleMaskClose} on:movetouch={handleMoveTouch}></div>
    <div class={isShow ? "weui-actionsheet weui-actionsheet_toggle" : "weui-actionsheet"}>
        { #if title && type === 'ios' }
        <div class="weui-actionsheet__title">
            <p class="weui-actionsheet__title-text">{ title }</p>
        </div>
        { /if }
        <div class="weui-actionsheet__menu">
            { #each menu as item }
            <div class="weui-actionsheet__cell" on:click={() => {handleMenuItemClick(item.value);}}>{item.text}</div>
            { /each }
        </div>
        <div class="weui-actionsheet__action">
            <div class="weui-actionsheet__cell" on:click={() => { handleClose(); }}>取消</div>
        </div>
    </div>
</div>
