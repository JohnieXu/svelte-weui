<script>
  import Alert from "./Alert.svelte";
  import Article from "./Article.svelte";
	import Gallery from "./Gallery.svelte";
  import ActionSheet from "./ActionSheet.svelte";
  import Dialog from "./Dialog.svelte";
  import Cells from "./components/Cell/Cells.svelte";
  import CellsTitle from "./components/Cell/CellsTitle.svelte";
  import Cell from "./components/Cell/Cell.svelte";
  import CellHeader from "./components/Cell/CellHeader.svelte";
  import CellBody from "./components/Cell/CellBody.svelte";
  import CellFooter from "./components/Cell/CellFooter.svelte";

	let isShowAlert = false;
	let isShowActionSheet = false;
  let actionSheetType = 'ios';
  let isShowDialog = false;
  let dialogType = 'ios';
  let dialogContent = '弹窗内容，告知当前状态、信息和解决方法，描述文字尽量控制在三行内';

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
  
  const showDialog = () => {
    dialogType = 'ios';
    isShowDialog = true;
  }

  const showAndroidDialog = () => {
    dialogType = 'android';
    isShowDialog = true;
  }
</script>

<style>
  .page {
    height: 100%;
    overflow: auto;
  }
  .page__hd {
    height: 100%;
    padding: 40px;
    overflow: auto;
  }
  .page__title {
    font-size: 0;
    margin-bottom: 15px;
  }
  .page_desc {
    margin-top: 4px;
    color: rgba(0,0,0,.5);
    text-align: left;
    font-size: 14px;
  }
</style>

<div class="page">
  <div class="page__hd">
    <div class="page__title">
      <img src="/weui.png" alt="WeUI" height="21" />
    </div>
    <p class="page_desc">
      WeUI
      是一套同微信原生视觉体验一致的基础样式库，由微信官方设计团队为微信内网页和微信小程序量身设计，令用户的使用感知更加统一。
    </p>
    <button class="weui-btn weui-btn_default" on:click={showAlert}>
      打开Alert
    </button>
		<button class="weui-btn weui-btn_default" on:click={showActionSheet}>
      打开ActionSheet
    </button>
		<button class="weui-btn weui-btn_default" on:click={showDialog}>
      打开Dialog
    </button>
    <button class="weui-btn weui-btn_default" on:click={showAndroidDialog}>
      打开Android Dialog
    </button>

    <Cells>
      <CellsTitle>标题</CellsTitle>
      <Cell access href="#">
        <CellHeader>header</CellHeader>
        <CellBody>body</CellBody>
        <CellFooter>footer</CellFooter>
      </Cell>
    </Cells>

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
    <Dialog
      type={dialogType}
      title={'不传递title则不展示标题'}
      content={dialogContent}
      isShow={isShowDialog}
      isMaskCancel={false}
      on:ok={e => {
        console.log(e.detail);
				isShowDialog = e.detail.isShow;
			}}
			on:cancel={e => {
        console.log(e.detail);
				isShowDialog = false;
			}}
    />

  </div>
</div>
