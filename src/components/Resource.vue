<template>
	<div class="box">
		<div class="card">
			<div class="card-content">
				<div class="media">
					<div class="media-content">
						<p class="title is-4">Discord Username</p>
					</div>
				</div>

				<div class="content">
					Text
				</div>
			</div>
		</div>
	</div>
</template>

<script lang="ts">

import {defineComponent} from 'vue';

export default defineComponent({
  name: 'Resource',
  components: { },
	props:{
		resource: Object,
	},
  setup(props) {

  }
});
</script>


<style scoped>

.box {
	max-width: 20vw;
}

</style>