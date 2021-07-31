<script>
	import NavBar from '../components/NavBar.svelte';

	import BaseOrgsCard from '../components/BaseOrgsCard.svelte';


	// import { dataset_dev } from 'svelte/internal';
</script>


	<NavBar />
	<div class="content-containers">
		<BaseOrgsCard />
	</div>


<style>
	.content-containers {
		display: flex;
		flex-direction: column;
		/* justify-content: center; */
		align-items: center;
		/* padding: 5rem; */

	}
	
	/* .main-layout {
		display: flex;
		
	} */
</style>
