<template>
	<view class="content">
		<view class="navget_bar">
			<uni-nav-bar :fixed="true" :statusBar="true" :border="false" color="#FFFFFF" background-color="#5D4037" right-icon="more-filled"
			 fontIcon="fuhao-shaixuan" @click-right="showDrawer('select')">
				<block slot="left">
					<view class="month">
						<picker mode="multiSelector" @columnchange="bindMultiPickerColumnChange"
						:value="multiIndex" :range="multiArray">
							<view class="uni-input">{{currentDate}}
								<uni-icons type="arrowdown" color="#FFFFFF" size="22" />
							</view>
						</picker>
					</view>
				</block>
			</uni-nav-bar>
		</view>
		<view class="status_bar"></view>
		<view class="bannar">
			<view class="title">11月支出</view>
			<view class="today-amount">500.00</view>
			<view class="in-out-amount">
				<text>收入</text>
				<text style="color: #FFF;">1000.00</text>
				<text>|</text>
				<text>结余</text>
				<text style="color: #FFF;">500.00</text>
			</view>
		</view>
		<uni-drawer :visible="isSelectDrawer" mode="right" @close="closeDrawer('select')">
			<view class="close select">
				<view class="status_bar status-drawer"></view>
				<view class="title">
					<uni-icons type="back" size="24" @click="closeDrawer('select')" color="#FFFFFF" />
					筛选
				</view>
				<uni-list>
					<uni-list-item title="时间" :context="selDate.msg" @click="showDrawer('date')"/>
					<uni-list-item title="类别" context="全部" @click="showDrawer('type')"/>
				</uni-list>
				<view class="amt">
					<view class="amt-title">金额区间</view>
					<view class="amt-context">
						<input class="amt-input" type="digit" />
						<view class="amt-split">-</view>
						<input class="amt-input" type="digit" />
					</view>
				</view>
				<view class="btn">
					<button class="mini-btn" type="default">重置</button>
					<button class="mini-btn" type="warn">保存</button>
				</view>
			</view>
		</uni-drawer>
		<uni-drawer :visible="isDateDrawer" mode="right" @close="closeDrawer('date')">
			<view class="close">
				<view class="status_bar status-drawer"></view>
				<view class="title">
					<uni-icons type="back" size="24" @click="closeDrawer('date')" color="#FFFFFF"/>
					时间
				</view>
				<scroll-view class="date" scroll-y="true">
					<view class="date">
						<uni-list>
							<uni-list-item title="全部" :show-arrow="false" :showChoose="dateAll" @click="dateChoose('all')"/>
						</uni-list>
						<uni-list class="list-tip">
							<uni-list-item title="今天" :show-arrow="false" :showChoose="dateToday" @click="dateChoose('today')"/>
							<uni-list-item title="昨天" :show-arrow="false" :showChoose="dateYesterday" @click="dateChoose('yesterday')"/>
						</uni-list>
						<uni-list class="list-tip">
							<uni-list-item title="最近七天" :show-arrow="false" :showChoose="dateSeven" @click="dateChoose('seven')"/>
							<uni-list-item title="最近三十天" :show-arrow="false" :showChoose="dateThirty" @click="dateChoose('thirty')"/>
							<uni-list-item title="最近一年" :show-arrow="false" :showChoose="dateYear" @click="dateChoose('year')"/>
						</uni-list>
						<uni-list class="list-tip">
							<uni-list-item title="本周" :show-arrow="false" :showChoose="dateWeek" @click="dateChoose('week')"/>
							<uni-list-item title="上周" :show-arrow="false" :showChoose="dateLastWeek" @click="dateChoose('lastWeek')"/>
						</uni-list>
						<uni-list class="list-tip">
							<uni-list-item title="本月" :show-arrow="false" :showChoose="dateMonth" @click="dateChoose('month')"/>
							<uni-list-item title="上月" :show-arrow="false" :showChoose="dateLastMonth" @click="dateChoose('lastMonth')"/>
						</uni-list>
						<uni-list class="list-tip">
							<uni-list-item title="本季" :show-arrow="false" :showChoose="dateQuarter" @click="dateChoose('quarter')"/>
							<uni-list-item title="上季" :show-arrow="false" :showChoose="dateLastQuarter" @click="dateChoose('lastQuarter')"/>
						</uni-list>
						<uni-list class="list-tip">
							<uni-list-item title="本年" :show-arrow="false" :showChoose="dateToyear" @click="dateChoose('toyear')"/>
							<uni-list-item title="去年" :show-arrow="false" :showChoose="dateLastYear" @click="dateChoose('lastYear')"/>
						</uni-list>
					</view>
				</scroll-view>
			</view>
		</uni-drawer>
		<uni-drawer :visible="isTypeDrawer" mode="right" @close="closeDrawer('type')">
			<view class="close">
				<view class="status_bar status-drawer"></view>
				<view class="title">
					<uni-icons type="back" size="24" @click="closeDrawer('type')" color="#FFFFFF" />
					类型
				</view>
				<view class="type-all">
					<lis-tree class="tree" :root="type.all" :checked="checked"
					show-checkbox auto-expand></lis-tree>
				</view>
				<scroll-view class="type" scroll-y="true">
					<div class="type">
						<view class="type-tip">支出</view>
						<lis-tree class="tree" :root="type.out" :checked="checked" :change-handler="checkChange" :check-handler="changeAllHandler"
						show-checkbox auto-expand></lis-tree>
						<view class="type-tip">收入</view>
						<lis-tree class="tree" :root="type.in" :checked="checked" :change-handler="checkChange" :check-handler="changeAllHandler"
						show-checkbox auto-expand></lis-tree>
					</div>
				</scroll-view>
			</view>
		</uni-drawer>
	</view>
</template>

<script>
	import uniIcons from '@/components/uni-icons/uni-icons.vue'
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'
	import uniDrawer from "@/components/uni-drawer/uni-drawer.vue"
	import uniList from '@/components/uni-list/uni-list.vue'
	import uniListItem from '@/components/uni-list-item/uni-list-item.vue'
	import lisTree from '@/components/lis-tree/lis-tree.vue'
	import formatter from '@/common/formatter.js';
	export default {
		components: {
			uniIcons,
			uniNavBar,
			uniDrawer,
			uniList,
			uniListItem,
			lisTree
		},
		onLoad: function() {
			console.log('App Load detail');  
	  },
		data() {
			return {
				city: '北京',
				currentDate:'本月',
				selDate:{
					msg:'本月',
					val:'month'
				},
				multiArray: [
					['2010', '2011', '2012', '2013', '2014', '2015', '2016', '2017', '2018','2019', '2020', '2021', '2022', '2023', '2024', '2025','2026', '2027', '2028', '2029', '2030'],
					['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12']
				],
				multiIndex: [0, 0],
				type: {
					all:{
						children: [{
								id: 'all',
								name: '全部',
								length: 10,
								check: 0
						}]
					},
					out:{
						children: [
							{
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
					in:{
						children: [
							{
								id: 'richangshouru',
								name: '日常收入',
								children: [{
									id: 'gongzixinshui',
									name: '工资薪水',
								},{
									id: 'jianzhiwaikuai',
									name: '兼职外快',
								},{
									id: 'hongbaolixi',
									name: '利息租金',
								},{
									id: 'yuebao',
									name: '余额宝',
								},{
									id: 'gupiaojijin',
									name: '股票基金',
								},{
									id: 'yingyeshouru',
									name: '营业收入',
								},{
									id: 'hongbaolijin',
									name: '红包礼金',
								},{
									id: 'canyinqita',
									name: '收入其他',
								} ]
							}
						]
					}
				},
				selected: null,
				checked: [],
				isSelectDrawer: false,
				isDateDrawer: false,
				isTypeDrawer: false,
				dateAll:true,
				dateToday:false,
				dateYesterday:false,
				dateSeven:false,
				dateThirty:false,
				dateYear:false,
				dateWeek:false,
				dateLastWeek:false,
				dateMonth:false,
				dateLastMonth:false,
				dateQuarter:false,
				dateLastQuarter:false,
				dateToyear:false,
				dateLastYear:false
			}
		},
		methods: {
			back() {
				uni.navigateBack({
					delta: 1
				})
			},
			showDrawer(s) {
				if(s == 'select'){
					this.isSelectDrawer = true;
				}else if(s == 'date'){
					this.isDateDrawer = true;
				}else if(s == 'type'){
					this.isTypeDrawer = true;
				}
			},
			closeDrawer(s) {
				if(s == 'select'){
					this.isSelectDrawer = false;
				}else if(s == 'date'){
					this.isDateDrawer = false;
				}else if(s == 'type'){
					this.isTypeDrawer = false;
				}
			},
			dateChoose( s) {
				this.dateAll=false;
				this.dateToday=false;
				this.dateYesterday=false;
				this.dateSeven=false;
				this.dateThirty=false;
				this.dateYear=false;
				this.dateWeek=false;
				this.dateLastWeek=false;
				this.dateMonth=false;
				this.dateLastMonth=false;
				this.dateQuarter=false;
				this.dateLastQuarter=false;
				this.dateToyear=false;
				this.dateLastYear=false;
				if(s == 'all'){
					this.dateAll = true;
					this.selDate.msg = '全部';
					this.selDate.val = 'all';
				}else if(s == 'today'){
					this.dateToday = true;
					this.selDate.msg = '今天';
					this.selDate.val = 'today';
				}else if(s == 'yesterday'){
					this.dateYesterday = true;
					this.selDate.msg = '昨天';
					this.selDate.val = 'yesterday';
				}else if(s == 'seven'){
					this.dateSeven = true;
					this.selDate.msg = '最近7天';
					this.selDate.val = 'seven';
				}else if(s == 'thirty'){
					this.dateThirty = true;
					this.selDate.msg = '最近30天';
					this.selDate.val = 'thirty';
				}else if(s == 'year'){
					this.dateYear = true;
					this.selDate.msg = '昨天';
					this.selDate.val = 'yesterday';
				}else if(s == 'week'){
					this.dateWeek = true;
					this.selDate.msg = '本周';
					this.selDate.val = 'week';
				}else if(s == 'lastWeek'){
					this.dateLastWeek = true;
					this.selDate.msg = '上周';
					this.selDate.val = 'lastWeek';
				}else if(s == 'month'){
					this.dateMonth = true;
					this.selDate.msg = '本月';
					this.selDate.val = 'month';
				}else if(s == 'lastMonth'){
					this.dateLastMonth = true;
					this.selDate.msg = '上月';
					this.selDate.val = 'lastMonth';
				}else if(s == 'quarter'){
					this.dateQuarter = true;
					this.selDate.msg = '本季';
					this.selDate.val = 'quarter';
				}else if(s == 'lastQuarter'){
					this.dateLastQuarter = true;
					this.selDate.msg = '上季';
					this.selDate.val = 'lastQuarter';
				}else if(s == 'toyear'){
					this.dateToyear = true;
					this.selDate.msg = '今年';
					this.selDate.val = 'toyear';
				}else if(s == 'lastYear'){
					this.dateLastYear = true;
					this.selDate.msg = '去年';
					this.selDate.val = 'lastYear';
				}
				// this.currentDate = this.selDate.msg;
				this.closeDrawer('date');
			},
			bindMultiPickerColumnChange(e) {
				console.log('修改的列为：' + e.detail.column + '，值为：' + e.detail.value)
				this.multiIndex[e.detail.column] = e.detail.value
				let chickDate = this.multiArray[0][this.multiIndex[0]]+'/'+this.multiArray[1][this.multiIndex[1]];
				console.log("当前值:"+chickDate)
				if(chickDate == new Date().getFullYear()+'/'+(new Date().getMonth()+1)){
					this.currentDate = '本月';
				}else{
					this.currentDate=chickDate;
				}
				this.$forceUpdate()
			},
			checkChange(e){
				console.info("点击了：");
				console.info(e);
			},
			changeAllHandler(e){
				console.info("AA点击了：");
				console.info(e);
			}
		},
		onPullDownRefresh() {
			console.log('onPullDownRefresh')
			setTimeout(function() {
				uni.stopPullDownRefresh()
				console.log('stopPullDownRefresh')
			}, 1000)
		}
	}
</script>

<style>
	.bannar {
		width: 96vw;
		height: 260rpx;
		overflow: hidden;
		flex-direction: column;
		background-color: #795548;
		color:#FFFFFF;
		box-shadow: 0 1px 2px #2E211C;
		padding-left: 4vw;
	}
	.month {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		width: 100%;
		margin-left: 15px;
		white-space: nowrap;
	}
	.bannar .title{
		/* flex-direction: row; */
		align-items: flex-end;
		height:70rpx;
		font-size: 14px;
		color: #C8C7CC;
	}
	.bannar .today-amount{
		height:120rpx;
		line-height: 120rpx;
		font-size: 30px;
		font-weight: bold;
	}
	.bannar .in-out-amount{
		height:70rpx;
		font-size: 14px;
		color: #C8C7CC;
	}
	.bannar .in-out-amount text{margin-right:3px;}
	.close{
		flex: 1;
		height: 100%;
		flex-direction: column;
	}
	.close .title{
		height:44px;
		color: #FFFFFF;
		line-height: 44px;
		background-color: #5D4037;
	}
	.close .btn{
		flex-direction: row;
		margin-top: 100rpx;
	}
	.close .btn .mini-btn{
		height: 74rpx;
		line-height: 74rpx;
		font-size: 30rpx;
		width: 180rpx;
	}
	.close .uni-list-item{
		padding: 0 10px;
		height: 120rpx;
		line-height: 120rpx;
	}
	.close .uni-list-item .uni-list-item__container{
		border-top-color: #F1F1F1 !important;
		padding:40rpx 5rpx 40rpx 2rpx !important;
	}
	.close .amt{
		flex-direction: column;
		margin: 0 22rpx;
		border-top: #F1F1F1 solid thin;
	}
	.close .amt-title{
		height: 72rpx;
		line-height: 72rpx;
		font-size: 34rpx;
		color: #222222;
	}
	.close .amt-context{
		padding-top: 40rpx;
	}
	.close .amt-split{
		padding: 0 24rpx;
		height: 64rpx;
		line-height: 64rpx;
		color: #999999;
	}
	.close .amt-input{
		width:180rpx;
		height: 64rpx;
		line-height: 64rpx;
		border-radius: 10rpx;
		background-color: #F1F1F1;
		text-align: center;
	}
	.close .date{
		height: 85%;
		background-color: #EFEFEF;
		flex-direction: column;
	}
	.close .list-tip{
		margin-top: 15rpx;
	}
	.close .type-all{
		display: flex;
		font-size: 30rpx;
		flex-direction: column;
	}
	.close .type{
		display: block;
		height: 78vh;
		/* background-color: #EFEFEF; */
	}
	.close .type .type-tip{
		display: block;
		padding: 15rpx 18rpx;
		font-size: 26rpx;
		background-color: #EFEFEF;
	}
	.close .type .tree{
		font-size: 30rpx;
		background-color: #F8F8F8;
	}
</style>
