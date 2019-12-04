<template>
	<div class="type" style="display: block;">
		<!-- <div style="height: 100vh">
			<h1> 单选 </h1>
			<lis-tree class="tree" :root="root" :selected="selected" show-radio :change-handler="onChange" auto-expand></lis-tree>
		</div>

		<div style="height: 100vh">
			<h1> 单选, 只显示叶子节点 </h1>
			<lis-tree class="tree" :root="root" :selected="selected" show-radio :change-handler="onChange" leaf-only auto-expand></lis-tree>
		</div> -->
		
		<lis-tree class="tree" :root="root.out" :checked="checked"
		show-checkbox :change-handler="onChange" auto-expand></lis-tree>
		<!-- <div style="height: 100vh">
			<h1> 多选, 只显示叶子节点 </h1>
			<lis-tree class="tree" :root="root" :checked="checked" show-checkbox :change-handler="onChange" leaf-only
			 auto-expand></lis-tree>
		</div> -->
	</div>
</template>

<script>
	import lisTree from '@/components/lis-tree/lis-tree.vue'
	export default {
		components: {
			lisTree
		},
		data() {
			return {
				root: {
					out:{children: [{
							id: 'canyin',
							name: '餐饮',
							children: [{
								id: 'zaocan',
								name: '早餐',
							},{
								id: 'wucan',
								name: '午餐',
							},{
								id: 'wancan',
								name: '晚餐',
							},{
								id: 'xiaoye',
								name: '宵夜',
							},{
								id: 'lingshi',
								name: '零食',
							},{
								id: 'yinliaoshuiguo',
								name: '饮料水果',
							},{
								id: 'maicaiyuanliao',
								name: '买菜原料',
							},{
								id: 'youyanjiangcu',
								name: '油盐酱醋',
							},{
								id: 'canyinqita',
								name: '餐饮其他',
							}, ]
						},
						{
							id: 'jiaotong',
							name: '交通',
							children: [{
								id: 'dache',
								name: '打车'
							},{
								id: 'gongjiao',
								name: '公交'
							},{
								id: 'ditie',
								name: '地铁'
							},{
								id: 'huoche',
								name: '火车'
							},{
								id: 'feiji',
								name: '飞机'
							},{
								id: 'zixingche',
								name: '自行车'
							},{
								id: 'changtuqiche',
								name: '长途汽车'
							},{
								id: 'jiayou',
								name: '加油'
							},{
								id: 'tingchefei',
								name: '停车费'
							},{
								id: 'baoyangweixiu',
								name: '保养维修'
							},{
								id: 'guoluguoqiao',
								name: '过路过桥'
							},{
								id: 'chekuanchedai',
								name: '车款车贷'
							},{
								id: 'jiaotongqita',
								name: '交通其他'
							} ]
						},
						{
							id: 'gouwu',
							name: '购物',
							children: [{
								id: 'chaoshi',
								name: '超市购物'
							},{
								id: 'fushixiebao',
								name: '服饰鞋包'
							},{
								id: 'jiajubaihuo',
								name: '家居百货'
							},{
								id: 'baobaoyongpin',
								name: '宝宝用品'
							},{
								id: 'huazhuanghufu',
								name: '化妆护肤'
							},{
								id: 'dianzishuma',
								name: '电子数码'
							},{
								id: 'zhubaoshoushi',
								name: '珠宝首饰'
							},{
								id: 'baojianyongpin',
								name: '保健用品'
							},{
								id: 'gouwuqita',
								name: '购物其他'
							}]
						},
						{
							id: 'yule',
							name: '娱乐',
							children: [{
								id: 'dianyinkge',
								name: '电影K歌'
							},{
								id: 'lvyoudujia',
								name: '旅游度假'
							},{
								id: 'yundongjianshen',
								name: '运动健身'
							},{
								id: 'majiangqipai',
								name: '麻将棋牌'
							},{
								id: 'yuleqita',
								name: '娱乐其他'
							}]
						},
						{
							id: 'yijiao',
							name: '医教',
							children: [{
								id: 'baoxianbaofei',
								name: '保险保费'
							},{
								id: 'yiliaoyongpin',
								name: '医疗用品'
							},{
								id: 'guahaomenzhen',
								name: '挂号门诊'
							},{
								id: 'yangshenbaojian',
								name: '养身保健'
							},{
								id: 'xuezajiaocai',
								name: '学杂教材'
							},{
								id: 'peixunkaoshi',
								name: '培训考试'
							},{
								id: 'youerjiaoyu',
								name: '幼儿教育'
							},{
								id: 'jiajiaobuxi',
								name: '家教补习'
							},{
								id: 'yijiaoqita',
								name: '医教其他'
							}]
						},
						{
							id: 'shenghuo',
							name: '生活',
							children: [{
								id: 'shoujidianhua',
								name: '手机电话'
							},{
								id: 'shuidianranqi',
								name: '水电燃气'
							},{
								id: 'zhusuzufang',
								name: '住宿租房'
							},{
								id: 'meirongmeifa',
								name: '美容美发'
							},{
								id: 'youzhengkuaidi',
								name: '邮政快递'
							},{
								id: 'diannaokuandai',
								name: '电脑宽带'
							},{
								id: 'jiazhengfuwu',
								name: '家政服务'
							},{
								id: 'fangkuanfangdai',
								name: '房款房贷'
							},{
								id: 'zhuangxiucaigou',
								name: '装修采购'
							},{
								id: 'shenghuoqita',
								name: '生活其他'
							}]
						},
						{
							id: 'renqing',
							name: '人情',
							children: [{
								id: 'wupin',
								name: '物品'
							},{
								id: 'xiaojing',
								name: '孝敬'
							},{
								id: 'qingke',
								name: '请客'
							},{
								id: 'lijinhongbao',
								name: '礼金红包'
							},{
								id: 'renqingqita',
								name: '人情其他'
							}]
						},
						{
							id: 'shengyi',
							name: '生意',
							children: [{
								id: 'yunyingfei',
								name: '运营费'
							},{
								id: 'huiwufei',
								name: '会务费'
							},{
								id: 'jinhuocaigou',
								name: '进货采购'
							},{
								id: 'rengongzhichu',
								name: '人工支出'
							},{
								id: 'caigoufuzhu',
								name: '材料辅助'
							},{
								id: 'jiaotongyunshu',
								name: '交通运输'
							},{
								id: 'gongchengfukuan',
								name: '工程付款'
							},{
								id: 'dianmianzujin',
								name: '店面租金'
							},{
								id: 'zhucedengji',
								name: '注册登记'
							},{
								id: 'shengyiqita',
								name: '生意其他'
							}]
						},
						{
							id: 'touzi',
							name: '投资',
							children: [{
								id: 'jijin',
								name: '基金'
							},{
								id: 'gupiao',
								name: '股票'
							},{
								id: 'P2P',
								name: 'P2P'
							},{
								id: 'yuebao',
								name: '余额宝'
							},{
								id: 'licaichanpin',
								name: '理财产品'
							},{
								id: 'touzidaikuan',
								name: '投资贷款'
							},{
								id: 'yinhangcunkuan',
								name: '银行存款'
							},{
								id: 'touziqita',
								name: '投资其他'
							}]
						},
					]
				},
					in:{}
				},
				selected: null,
				checked: [],
			}
		},
		methods: {
			onChange(selected) {
				console.log(selected)
			}
		},
		onLoad() {
			setTimeout(() => {
				this.root.out = {
					children: [{
							id: 'canyin',
							name: '餐饮',
							children: [{
								id: 'zaocan',
								name: '早餐',
							},{
								id: 'wucan',
								name: '午餐',
							},{
								id: 'wancan',
								name: '晚餐',
							},{
								id: 'xiaoye',
								name: '宵夜',
							},{
								id: 'lingshi',
								name: '零食',
							},{
								id: 'yinliaoshuiguo',
								name: '饮料水果',
							},{
								id: 'maicaiyuanliao',
								name: '买菜原料',
							},{
								id: 'youyanjiangcu',
								name: '油盐酱醋',
							},{
								id: 'canyinqita',
								name: '餐饮其他',
							}, ]
						},
						{
							id: 'jiaotong',
							name: '交通',
							children: [{
								id: 'dache',
								name: '打车'
							},{
								id: 'gongjiao',
								name: '公交'
							},{
								id: 'ditie',
								name: '地铁'
							},{
								id: 'huoche',
								name: '火车'
							},{
								id: 'feiji',
								name: '飞机'
							},{
								id: 'zixingche',
								name: '自行车'
							},{
								id: 'changtuqiche',
								name: '长途汽车'
							},{
								id: 'jiayou',
								name: '加油'
							},{
								id: 'tingchefei',
								name: '停车费'
							},{
								id: 'baoyangweixiu',
								name: '保养维修'
							},{
								id: 'guoluguoqiao',
								name: '过路过桥'
							},{
								id: 'chekuanchedai',
								name: '车款车贷'
							},{
								id: 'jiaotongqita',
								name: '交通其他'
							} ]
						},
						{
							id: 'gouwu',
							name: '购物',
							children: [{
								id: 'chaoshi',
								name: '超市购物'
							},{
								id: 'fushixiebao',
								name: '服饰鞋包'
							},{
								id: 'jiajubaihuo',
								name: '家居百货'
							},{
								id: 'baobaoyongpin',
								name: '宝宝用品'
							},{
								id: 'huazhuanghufu',
								name: '化妆护肤'
							},{
								id: 'dianzishuma',
								name: '电子数码'
							},{
								id: 'zhubaoshoushi',
								name: '珠宝首饰'
							},{
								id: 'baojianyongpin',
								name: '保健用品'
							},{
								id: 'gouwuqita',
								name: '购物其他'
							}]
						},
						{
							id: 'yule',
							name: '娱乐',
							children: [{
								id: 'dianyinkge',
								name: '电影K歌'
							},{
								id: 'lvyoudujia',
								name: '旅游度假'
							},{
								id: 'yundongjianshen',
								name: '运动健身'
							},{
								id: 'majiangqipai',
								name: '麻将棋牌'
							},{
								id: 'yuleqita',
								name: '娱乐其他'
							}]
						},
						{
							id: 'yijiao',
							name: '医教',
							children: [{
								id: 'baoxianbaofei',
								name: '保险保费'
							},{
								id: 'yiliaoyongpin',
								name: '医疗用品'
							},{
								id: 'guahaomenzhen',
								name: '挂号门诊'
							},{
								id: 'yangshenbaojian',
								name: '养身保健'
							},{
								id: 'xuezajiaocai',
								name: '学杂教材'
							},{
								id: 'peixunkaoshi',
								name: '培训考试'
							},{
								id: 'youerjiaoyu',
								name: '幼儿教育'
							},{
								id: 'jiajiaobuxi',
								name: '家教补习'
							},{
								id: 'yijiaoqita',
								name: '医教其他'
							}]
						},
						{
							id: 'shenghuo',
							name: '生活',
							children: [{
								id: 'shoujidianhua',
								name: '手机电话'
							},{
								id: 'shuidianranqi',
								name: '水电燃气'
							},{
								id: 'zhusuzufang',
								name: '住宿租房'
							},{
								id: 'meirongmeifa',
								name: '美容美发'
							},{
								id: 'youzhengkuaidi',
								name: '邮政快递'
							},{
								id: 'diannaokuandai',
								name: '电脑宽带'
							},{
								id: 'jiazhengfuwu',
								name: '家政服务'
							},{
								id: 'fangkuanfangdai',
								name: '房款房贷'
							},{
								id: 'zhuangxiucaigou',
								name: '装修采购'
							},{
								id: 'shenghuoqita',
								name: '生活其他'
							}]
						},
						{
							id: 'renqing',
							name: '人情',
							children: [{
								id: 'wupin',
								name: '物品'
							},{
								id: 'xiaojing',
								name: '孝敬'
							},{
								id: 'qingke',
								name: '请客'
							},{
								id: 'lijinhongbao',
								name: '礼金红包'
							},{
								id: 'renqingqita',
								name: '人情其他'
							}]
						},
						{
							id: 'shengyi',
							name: '生意',
							children: [{
								id: 'yunyingfei',
								name: '运营费'
							},{
								id: 'huiwufei',
								name: '会务费'
							},{
								id: 'jinhuocaigou',
								name: '进货采购'
							},{
								id: 'rengongzhichu',
								name: '人工支出'
							},{
								id: 'caigoufuzhu',
								name: '材料辅助'
							},{
								id: 'jiaotongyunshu',
								name: '交通运输'
							},{
								id: 'gongchengfukuan',
								name: '工程付款'
							},{
								id: 'dianmianzujin',
								name: '店面租金'
							},{
								id: 'zhucedengji',
								name: '注册登记'
							},{
								id: 'shengyiqita',
								name: '生意其他'
							}]
						},
						{
							id: 'touzi',
							name: '投资',
							children: [{
								id: 'jijin',
								name: '基金'
							},{
								id: 'gupiao',
								name: '股票'
							},{
								id: 'P2P',
								name: 'P2P'
							},{
								id: 'yuebao',
								name: '余额宝'
							},{
								id: 'licaichanpin',
								name: '理财产品'
							},{
								id: 'touzidaikuan',
								name: '投资贷款'
							},{
								id: 'yinhangcunkuan',
								name: '银行存款'
							},{
								id: 'touziqita',
								name: '投资其他'
							}]
						},
					]
				}
			}, 1000)
		},

	}
</script>

<style>
	h1 {
		color: red;
	}
	.type{
		width: 750rpx;
		height: 100vh;
		align-items: flex-start;
	}
	.tree{
		width: 750rpx;
		background-color: #F8F8F8;
	}
</style>