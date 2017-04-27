<template>
	<div>
		<button v-if="$route.path !== '/time-entries/log-time'" v-link="'/time-entries/log-time'" class="btn btn-primary"></button>
		<div v-if="$route.path === '/time-entries/log-time'">
			<h3>创建</h3>
		</div>
		<hr>
		<router-view></router-view>
		<div class="time-entries">
			<p v-if="!timeEntries.length">
				<strong>还没有任何任务</strong>
			</p>
			<div class="list-group">
				<a class="list-group-item" v-for="timeEntry in timeEntries">
					<div class="row">
						<div class="col-sm-2 user-details">
							<img :src="timeEntry.user.image" class="avatar img-circle img-responsive"/>
							<p class="text-center">
								<strong>
									{{timeEntry.user.name}}
								</strong>
							</p>
						</div>
						<div class="col-sm-2 text-center time-block">
							<h3 class="list-group-item-text total-time">
								<i class="glyphicon glyphicon-time"></i>
								{{timeEntry.totalTime}}
							</h3>
							<p class="label label-primary text-center">
								<i class="glyphicon glyphicon-calendar"></i>
								{{timeEntry.date}}
							</p>
						</div>
						<div class="col-sm-7 comment-section">
							<p>{{timeEntry.comment}}</p>
						</div>
						<div class="col-sm-1">
							<button class="btn btn-xs btn-danger delete-button" @click="deleteTimeEntry(timeEntry)">
								X
							</button>
						</div>
					</div>
				</a>
			</div>
		</div>
	</div>
</template>
<script>
	export default{
		data(){
			let exisingEntry={
				user:{
					name:'二哲',
					email:'kodo@forchange.cn',
					image:'https://sfault-avatar.b0.upaiyun.com/888/223/888223038-5646dbc530_huge256'
				},
				comment:'我的一个备注',
				totalTime:1.5,
				date:'2017-04-27'
			}
			return{
				timeEntries:[existingEntry]
			}
		},
		methods:{
			deleteTimeEntry(timeEntry){
				let index = this.timeEntries.indexOf(timeEntry)
				if(window.confirm('确定要删除吗？')){
					this.timeEntries.splice(index,1)
					this.$dispath('deteteTime',timeEntry)
				}
			}
		},
		events:{
			timeUpdate(timeEntry){
				this.timeEntries.push(timeEntry)
				return true
			}
		}
	}

</script>
<style>
	.avatar{
		height:75px;
		margin:0 auto;
		margin-top:10px;
		margin-bottom:10px;
	}
	.user-details{
		background-color:#f5f5f5;
		border-right:1px solid #ddd;
		magin:-10px 0;
	}
	.time-block{
		padding:10px;
	}
	.comment-section{
		padding:20px;
	}
</style>