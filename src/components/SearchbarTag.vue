<template>
	<span class="tag" :class="{ 'is-danger': !this.selected, 'is-info': this.selected }" @click="tagSelected">
		{{tag}}
	</span>
</template>

<script>
export default {
  name: 'SearchbarTag',
	props:{
		tag: String,
		selected: Boolean
	},
	methods:{
		tagSelected(){
			this.$emit("tag-selected", {tag: this.tag})
		}
	}
}
</script>

<style scoped>
.tag{
	cursor:pointer;
}
</style>