<template>
	<div class='movie_classic'>
		<div class='movie_classic_left'>
			<div class='movie_classic_left_title'>经典影视</div>
			<div class='movie_classic_list'>
				<ul>
					<li :class='{list:flag==i||f==i}' v-for='(item,i) in movieSoonList' :key='item.id'>
						<a href="#">
							<img :src="item.img">
						</a>
						<div>
							<span>{{ item.name }}</span>
							<i>{{ item.score }}</i>
						</div>
					</li>
				</ul>
			</div>
		</div>
		<div class='movie_classic_right'>
			<div class='movie_classic_right_title'>经典排行</div>
			<div class='movie_classic_ranking_list'>
				<ul>
					<li v-for='(item,i) in movieClassicList' :key='item.id' :class='{li_height:index==i}' @mouseenter='getindex(i)'>
						<div class='movie_classic_ranking_list_index1' v-if='index==i'>
							<div><a href="#"><img :src="item.img"></a>
							</div>
							<div>
								<p><a href="#">{{ item.name }}</a><span>{{ item.score }}</span></p>
								<p><a href="#">{{ item.performer }}</a></p>
								<p>
									<b>{{ item.serial }}</b>
									<span>{{ item.hot }}</span>
									<span>{{ item.type }}</span>
								</p>
							</div>
						</div>
						<div v-show='index!=i'>
							<i :class='{color:i<3}'>{{ item.serial }}</i>
							<span>{{ item.name }}</span>
							<span>{{ item.hot }}</span>
						</div>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return {
				flag:0,
				f:4,
				index:0,
				movieSoonList:[],
				movieClassicList:[]
			}
		},
		created(){
			this.getMovieSoon();
			this.getMovieClassic()
		},
		methods:{
			getMovieSoon(){
				this.axios.get('/src/data/movie_data/classic_movies.json').then(res=>{
					this.movieSoonList=res.data
				})
			},
			getMovieClassic(){
				this.axios.get('/src/data/movie_data/classsic_ranking.json').then(res=>{
					this.movieClassicList=res.data
				})
			},
			getindex(i){
				this.index=i
			}
		}
	}
</script>

<style lang='less' scoped>
	.movie_classic{
		width: 1200px;
		margin: 0 auto;
		overflow: hidden;
		.movie_classic_left{
			width: 840px;
			float: left;
			overflow: hidden;
			.movie_classic_left_title{
				height: 80px;
				width: 840px;
				font-size: 24px;
				line-height: 80px;
			}
			.movie_classic_list{
				ul{
					li{
						width: 160px;
						height: 250px;
						position: relative;
						margin-left: 48px;
						float: left;
						a{
							img{
								width: 158px;
								height: 210px;
								display: block;
								border-radius: 4px;
							}
						}
						div{
							width: 158px;
							height: 30px;
							position: absolute;
							bottom: 40px;
							background-color: rgba(0,0,0,.7);
							span{
								display: inline-block;
								text-align: center;
								line-height: 30px;
								font-size: 15px;
								width: 118px;
								height: 30px;
								color: #fff;
								text-overflow: ellipsis;
								overflow: hidden;
								white-space: nowrap;
							}
							i{
								display: inline-block;
								width: 35px;
								height: 30px;
								line-height: 30px;
								color:#ffb400;
								float: right;
							}
						}
					}
					.list{
							margin-left: 0;
						}
				}
			}
		}
		.movie_classic_right{
			float: right;
			width: 360px;
			.movie_classic_right_title{
				height: 80px;
				width: 360px;
				font-size: 24px;
				line-height: 80px;
			}
			.movie_classic_ranking_list{
				ul{
					.li_height{
						height: 126px;
					}
					li{
						width: 360px;
						height: 35px;
						margin-bottom: 10px;
						line-height: 35px;
						div:last-child{
							i{
								display: inline-block;
								width: 25px;
								height: 35px;
								color: #aaa;
							}
							.color{
								color: #FF4B00;
							}
							span:first-child{
								color: #333;
								font-size: 15px;
							}
							span:last-child{
								float: right;
								color: #ff4b00;
							}
						}
						.movie_classic_ranking_list_index1{
							width: 360px;
							height: 126px;
							position: relative;
							div:first-child{
								width:93px;
								height: 124px;
								float: left;
								img{
									width: 100%;
									height: 100%;
								}
							}
							div:last-child{
								width: 250px;
								height: 126px;
								float: right;
								p{
									font-size: 14px;
									line-height: 25px;
									display: -webkit-box;
									-webkit-box-orient: vertical;
									-webkit-line-clamp: 2;
									overflow: hidden;
									a{
										color: #333;
									}
								}
								p:first-child{
									font-size: 16px;
									line-height: 35px;
									span{
										color: #ff4b00;
										font-weight: bold;
										display: inline-block;
										float: right;
									}
								}
								p:last-child{
									line-height: 35px;
									span{
										color: red;
									}
									span:last-child{
										float: right;
									}
									b{
										display: inline-block;
										width: 25px;
										height: 30px;
										text-align: center;
										line-height: 30px;
										position: absolute;
										top: 0;
										left: 0;
										background-color: #ff4b00;
										color: #fff;
									}
								}
							}
							
						}
					}
				}
			}
		}
	}
</style>