<template>
	<span class="tag is-info">
		{{tag}}
	</span>
</template>

<script>
export default {
  name: 'ResourceTag',
	props:{
		tag: String,
	},
}
</script>