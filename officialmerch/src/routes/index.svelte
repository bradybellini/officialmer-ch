<script>
	import supabase from '$lib/db';

	async function getOrgs() {
		return supabase.from('organization').select(`name`).eq('is_public', true);
	}
</script>

{#await getOrgs()}
	Loading..
{:then response}
	<pre>{JSON.stringify(response, null, 2)}</pre>
{/await}
