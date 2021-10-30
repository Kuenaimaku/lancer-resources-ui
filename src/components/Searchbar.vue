<template>
	<div class="columns is-centered">
		<div class="column is-two-fifths">
			<div class="field">
				<label class="label">Title</label>
				<div class="control">
					<input class="input" type="text" placeholder="Search through titles" v-model="search.title">
				</div>
			</div>
		</div>
		<div class="column is-three-fifths">
			<div class="field">
				<label class="label">Tags</label>
				<p class="control tags">
					<SearchbarTag v-for="string in this.options.tags" 
						:key="string" 
						:tag="string" 
						:selected="this.search.tags.includes(string)"
						@tagSelected="parentEmit"/>
				</p>
			</div>
		</div>
	</div>
</template>

<script>
import SearchbarTag from './SearchbarTag.vue';
export default({
  name: 'Searchbar',
	components:{
		SearchbarTag
	},
	props:{
		search: Object,
		options: Object,
	},
	computed: {
		isSelected(string){
			return this.search.tags.indexOf(string) !== -1
		}
	},
	methods:{
		parentEmit(event){
			this.$emit("tag-selected", event)
		}
	}
});
</script>

<style>
p.control.tags {
    margin-top: 16px;
}
</style>