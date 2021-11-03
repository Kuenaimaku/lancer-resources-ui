<template>
	<div class="box">
		<div class="card">
			<div class="card-content">
				<div class="media-content">
					<p class="title is-4">{{resource.title}}</p>
					<p class="subtitle is-6">{{resource.author}}</p>
				</div>
			</div>
			<div class="content" v-html="this.resource.description.linkify()"></div>
			<div class="content">
				<button v-if="this.resource.url !== ''" class="button is-large is-fullwidth is-primary" @click.prevent="openUrl">Open Asset</button>
			</div>
			<div class="tags">
				<ResourceTag v-for="string in this.resource.tags" :key="string" :tag="string"/>
			</div>
		</div>
	</div>
</template>

<script>
import 'linkifyjs/lib/linkify-string'

import ResourceTag from './ResourceTag.vue'
export default({
  name: 'ResourceModal',
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
		},
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
	min-width:600px;
	max-width:60vw;
}

.card {
	padding: 2em;
}

.image img{
	object-fit: cover;
}

.content{
	white-space: pre-wrap;
}


</style>