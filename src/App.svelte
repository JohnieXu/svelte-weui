<script>
  import Alert from "./Alert.svelte";
  import Cell from "./Cell.svelte";
  import Article from "./Article.svelte";
	import Gallery from "./Gallery.svelte";
	import ActionSheet from "./ActionSheet.svelte";

	let isShowAlert = false;
	let isShowActionSheet = false;
	let actionSheetType = 'ios';

  let forms = ["Button", "Input", "List", "Slider", "Uploader"];
  let basics = [
    "Article",
    "Badge",
    "Flex",
    "Footer",
    "Gallery",
    "Grid",
    "Icons",
    "Loadmore",
    "Panel",
    "Preview",
    "Progress"
  ];
	let actions = ["Actionsheet", "Dialog", "Msg", "Picker", "Toast"];
	let navigators = ['Navbar', 'Tabbar']
	let searchs = ['Search Bar']

  const showAlert = () => {
    isShowAlert = true;
	};
	
	const showActionSheet = () => {
		// 通过函数式调用更改actionsheet组件显示类型
		actionSheetType = 'ios';
		isShowActionSheet = true;
	}
</script>

<style>
  .page__hd {
    padding: 40px;
  }
</style>

<div class="page">
  <div class="page__hd">
    <h1>WeUI</h1>
    <p>
      WeUI
      是一套同微信原生视觉体验一致的基础样式库，由微信官方设计团队为微信内网页和微信小程序量身设计，令用户的使用感知更加统一。
    </p>
    <button class="weui-btn weui-btn_default" on:click={showAlert}>
      打开Alert
    </button>
		<button class="weui-btn weui-btn_default" on:click={showActionSheet}>
      打开ActionSheet
    </button>
    <div class="weui-cells__title">表单</div>
    {#each basics as item (item)}
      <div class="weui-cells">
        <a class="weui-cell weui-cell_access" href="javascript:;">
          <div class="weui-cell__bd">
            <p>{item}</p>
          </div>
          <div class="weui-cell__ft" />
        </a>
      </div>
    {/each}

    <div class="weui-cells__title">基础组件</div>
    {#each forms as item (item)}
      <div class="weui-cells">
        <a class="weui-cell weui-cell_access" href="javascript:;">
          <div class="weui-cell__bd">
            <p>{item}</p>
          </div>
          <div class="weui-cell__ft" />
        </a>
      </div>
    {/each}

    <div class="weui-cells__title">操作反馈</div>
    {#each actions as item (item)}
      <div class="weui-cells">
        <a class="weui-cell weui-cell_access" href="javascript:;">
          <div class="weui-cell__bd">
            <p>{item}</p>
          </div>
          <div class="weui-cell__ft" />
        </a>
      </div>
    {/each}

    <div class="weui-cells__title">导航相关</div>
    {#each navigators as item (item)}
      <div class="weui-cells">
        <a class="weui-cell weui-cell_access" href="javascript:;">
          <div class="weui-cell__bd">
            <p>{item}</p>
          </div>
          <div class="weui-cell__ft" />
        </a>
      </div>
    {/each}

    <div class="weui-cells__title">搜索相关</div>
    {#each searchs as item (item)}
      <div class="weui-cells">
        <a class="weui-cell weui-cell_access" href="javascript:;">
          <div class="weui-cell__bd">
            <p>{item}</p>
          </div>
          <div class="weui-cell__ft" />
        </a>
      </div>
    {/each}

    <div class="weui-cells__title">层级规范</div>

    <Alert
      isShow={isShowAlert}
      on:ok={e => {
        isShowAlert = e.detail.isShow;
      }} />
		<ActionSheet
			type={actionSheetType}
			title={ '这是一个标题，可以为一行或者两行。' }
			menu={[
				{
					text: '菜单项一',
					value: 1
				},
				{
					text: '菜单项二',
					value: 2
				}
			]}
			isShow={isShowActionSheet}
			on:ok={e => {
				isShowActionSheet = e.detail.isShow;
			}}
			on:cancel={e => {
				isShowActionSheet = false;
			}}
		/>

  </div>
</div>
