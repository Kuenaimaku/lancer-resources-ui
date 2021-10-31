<template>
	<div class="box">
		<div class="card">
			<div class="card-image">
				<figure class="image is-16by9">
					<img :src="image" alt="Placeholder image">
				</figure>
			</div>
			<div class="card-content">
				<div class="media-content">
					<p class="title is-4">{{resource.title}}</p>
					<p class="subtitle is-6">{{resource.author}}</p>
				</div>
			</div>
			<div class="content">
				{{resource.description}}
			</div>
			<div class="content">
				<button class="button is-large is-fullwidth is-primary" @click.prevent="openUrl">Open Asset</button>
			</div>
			<div class="tags">
				<ResourceTag v-for="string in this.resource.tags" :key="string" :tag="string"/>
			</div>
		</div>
	</div>
</template>

<script>
import ResourceTag from './ResourceTag.vue'
export default({
  name: 'Resource',
	components:{
		ResourceTag
	},
	props:{
		resource: Object,
	},
	computed: {
		image(){
			if (this.resource.image == ""){
				return "/placeholder.jpg"
			}
			return this.resource.image;
		}
	},
	methods: {
		openUrl(){
			window.open(this.resource.url, '_blank')
		}
	}
});
</script>


<style scoped>

.box {
	min-width:345px;
	max-width:370px;
}

.image img{
	object-fit: cover;
}

</style>