<template>
	<div class="box">
		<div class="card">
			<div class="card-image">
				<figure class="image is-16by9">
					<img :src="image" alt="Placeholder image" />
				</figure>
			</div>
			<div class="card-content">
				<div class="media-content">
					<p class="title is-4">{{ resource.title }}</p>
					<p class="subtitle is-6">{{ resource.author }}</p>
				</div>
			</div>
			<div class="content">{{ shortDescription }}</div>
			<div class="content">
				<button
					v-if="this.resource.description.length >= 400"
					class="button is-large is-fullwidth is-info"
					@click.prevent="openResourceModal"
				>Read More</button>
			</div>
			<div class="content">
				<button
					v-if="this.resource.url !== ''"
					class="button is-large is-fullwidth is-primary"
					@click.prevent="openUrl"
				>Open Asset</button>
			</div>
			<div class="tags">
				<ResourceTag v-for="string in this.resource.tags" :key="string" :tag="string" />
			</div>
		</div>
	</div>
</template>

<script>
import ResourceTag from './ResourceTag.vue'
import ResourceModal from './ResourceModal.vue'
export default (
	{
		name: 'Resource',
		components: {
			ResourceTag,
			ResourceModal
		},
		props: {
			resource: Object,
		},
		computed: {
			image() {
				if (this.resource.image == "") {
					return "/placeholder.jpg"
				}
				return this.resource.image;
			},
			shortDescription() {
				if (this.resource.description.length <= 425) { return this.resource.description; }
				const subString = this.resource.description.substr(0, 400-1); 
				return subString.substr(0, subString.lastIndexOf(" "))  + "...";
			}
		},
		methods: {
			openUrl() {
				window.open(this.resource.url, '_blank')
			},
			openResourceModal() {
				this.$oruga.modal.open({
					parent: this,
					component: ResourceModal,
					custom: true,
					trapFocus: true,
					props: {
						resource: this.resource,
					},
					class: "resource-modal",
					width: 1920,
				});
			},
		},
	}
);
</script>


<style scoped>
.box {
	min-width: 345px;
	max-width: 370px;
}
.image img {
	object-fit: cover;
}

.content{
	white-space: pre-wrap;
}

</style>