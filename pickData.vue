<template>
	<div class="pd-basic">
		<div class="pd-show" @click="isShow = true">
			{{pick_data}}
		</div>
		<div class="pickData" v-if="isShow" @click.self="isShow =false">
			<div class="pd-content">
				<div class="pd-top">
					<div class="pd-box" @click="last">
						<div class="pd-left"></div>
					</div>
					<div class="pd-box">
						<span class="pd-month">{{cur_data.month+1 }}</span>
						<span class="pd-year"> -{{cur_data.year}}</span>
					</div>
					<div class="pd-box" @click="next">
						<div class="pd-right"></div>
					</div>
				</div>
				<div class="pd-middle" v-if="dayList.length>0">
					<span>周日</span>
					<span>周一</span>
					<span>周二</span>
					<span>周三</span>
					<span>周四</span>
					<span>周五</span>
					<span>周六</span>

					<span v-for="(item,index) in dayList" class="pd-day" :class='{nothismonth:isTrue(item.month)}' @click="pickData(item)">
						{{item.day}}
					</span>
				</div>
				<div class="pd-bottom">
					<div @click="today">Today</div>
					<div @click="clear">Clear</div>
					<div @click="close">Close</div>
				</div>
			</div>
		</div>	
	</div>
	
</template>
<script type="text/javascript">
	export default{
		props:{
			
		},
		watch:{
			pick_data(newD,old){
				this.$emit('pickdate',newD);
			}
		},
		data(){
			return{
				pick_data:'请选择日期',
				cur_data:{
					month:null,
					year:null
				},
				isShow:false,
				month:[31,28,31,30,31,30,31,31,30,31,30,31],
				dayList:[]
			}
		},
		methods:{
			isTrue(mon){
				if(mon == this.cur_data.month)
					return false
				return true
			},
			pickData(item){
				this.pick_data = item.year + '-' + (item.month+1) +'-' +item.day;
				this.isShow = false;
			},
			showCurData(){
				console.log(this.cur_data);
			},
			calcData(){
				var curYear = this.cur_data.year;
				var curMonth = this.cur_data.month;
				
				if((curYear/100)%1 == 0 ) 
				{
					if( (curYear/400)%1 == 0)
						this.month[1] = 29;
					else
						this.month[1] = 28;
				}else{
					if((curYear/4)%1 == 0)
						this.month[1] = 29;
					else
						this.month[1] = 28;
				}

				var curday = this.month[curMonth];

				var newDate = new Date(curYear,curMonth,1);
				var firstDay = newDate.getDay();

				this.daylist = [];

				var lastMonth,lastMonthDay,lastYear,nextYear,nextMonth,nextDay = 1,newDayList =[],i;

				if(curMonth == 0)
				{
					lastMonthDay = 31;
					lastMonth = 11;
					lastYear = curYear - 1;
				}else{
					lastYear = curYear;
					lastMonth = curMonth-1;
					lastMonthDay = this.month[lastMonth];
				}

				if(curMonth == 11)
				{
					nextMonth = 0;
					nextYear = curYear + 1;
				}else{
					nextMonth = curMonth + 1;
					nextYear = curYear;
				}

				for(i = firstDay-1;i>=0;i--)
				{
					var mes = {
						day:lastMonthDay--,
						month:lastMonth,
						year:lastYear
					}
					newDayList.unshift(mes);
				}
				for(i=1;i<=curday;i++)
				{
					var mes = {
						day:i,
						month:curMonth,
						year:curYear
					}
					newDayList.push(mes);
				}
				for( i = newDayList.length;i<42;i++)
				{
					var mes = {
						day:nextDay++,
						month:nextMonth,
						year:nextYear
					}
					newDayList.push(mes);
				}

				// console.log(newDayList);
				this.dayList = newDayList;
			},
			next(){
				console.log('next');
				var curMonth = this.cur_data.month;
				var curYear = this.cur_data.year;
				var nextMonth,nextYear;
				if(curMonth == 11)
				{
					nextMonth = 0;
					nextYear = curYear + 1;
				}else{
					nextMonth = curMonth + 1;
					nextYear = curYear;
				}
				this.cur_data.month = nextMonth;
				this.cur_data.year = nextYear;

				this.calcData();
			},
			last(){
				console.log('last');
				var curMonth = this.cur_data.month;
				var curYear = this.cur_data.year;
				var lastMonth,lastYear;
				if(curMonth == 0)
				{
					lastMonth = 11;
					lastYear = curYear - 1;
				}else{
					lastYear = curYear;
					lastMonth = curMonth-1;
				}

				this.cur_data.month = lastMonth;
				this.cur_data.year = lastYear;

				this.calcData();
			},
			today(){
				var  curData = new Date();
				this.pick_data = curData.getFullYear() + '-' + (curData.getMonth()+1) +'-' +curData.getDate();
				this.isShow = false;
			},
			clear(){
				this.pick_data ='请选择日期';
				this.isShow = false;
			},
			close(){
				this.isShow = false;
			},
		},
		mounted(){
			var  curData = new Date();
			this.cur_data.year = curData.getFullYear() ;
			this.cur_data.month = curData.getMonth()  ;
			this.calcData();
		}
	}
</script>
<style type="text/css" lang="less" scoped>
	.pd-basic{
		display: inline-block;
		width:100%;
		.pd-show{
			width:100%;
			cursor: pointer;
			border:1px solid #999999;
			color:#999999;
			padding:10px;
			font-weight: normal;
		}
	}
	.pickData{
		position: fixed;
		background-color: rgba(0,0,0,0.5);
		width:100%;
		height:100%;
		top:0px;
		left:0px;
		display: flex;
		justify-content: center;
		align-items: flex-end;
		.pd-content{
			display: flex;
			flex-direction: column;
			justify-content: space-between;
		
			width:650px;
			height:450px;
			background-color: white;
			box-shadow: 0 0 10px 1px rgba(0, 0, 0, 0.2);
			background-color: white;
			margin-bottom: 10%;
			.pd-top{
				display: flex;
				justify-content: space-between;
				.pd-box{
					flex:1;
					display: flex;
					justify-content: center;
					align-items: center;
					padding:10px 0px;
					.pd-left{
						width: 0;
						height:0;
						border-width: 15px 15px 15px 0px;
						border-color:transparent #999999 transparent transparent;
						border-style: solid;
					}
					.pd-right{
						width: 0;
						height:0;
						border-width: 15px 0px 15px 15px;
						border-color:transparent transparent transparent #999999;
						border-style: solid;
					}
				}
				.pd-box:first-child,.pd-box:last-child{
					cursor:pointer;
					&:hover{
						background-color: #f08086;
						.pd-left{
							border-right-color: white;
						}
						.pd-right{
							border-left-color: white;
						}
					}
					
				}
			}
			.pd-bottom{
				display: flex;
				justify-content: space-around;
				align-items: center;
				>div{
					cursor: pointer;
					flex:1;
					text-align: center;
					padding:10px 0;
					&:hover{
						background-color: #f08086;
						color:white;	
					}
					
				}
			}
			.pd-middle{
				display: flex;
				flex-wrap: wrap;
				span{
					flex:1 0 14.2%;
					display: flex;
					justify-content: center;
					align-items: center;
					padding:10px 0;
					color:#999999;
					
					
				}
				.pd-day{
					cursor: pointer;
					&:hover{
						background-color: #f08086;
						color:white;
					}
				}
				.nothismonth{
					color:#d6d6d6;
				}
			}
		}
	}
	@media screen and (max-width: 750px) {
		.pd-basic{
			.pd-show{
				padding:0.133333rem;
			}
		}
	}
</style>