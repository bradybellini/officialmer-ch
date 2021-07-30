<script lang="ts">
	import supabase from '$lib/db';
	import {
		Row,
		Col,
		Icon,
		Button,
		Card,
		CardHeader,
		CardBody,
		CardTitle,
		CardSubtitle,
		Image
	} from 'sveltestrap';
	async function getOrgs() {
		const publicOrgs = await supabase
			.from('organization')
			.select(`name, merch_url, official_url, is_nsfw, logo`)
			.eq('is_public', true);
		return publicOrgs;
	}
</script>

{#await getOrgs()}
	Loading..
{:then response}
	<div class="containter">
		<div class="row row-cols-10 g-4 ">
			{#each response.data as org}
				<div class="col">
					<div class="card bg-light border-dark" style="width: 15rem;">
						<div class="d-flex flex-column align-items-center m-2">
							<!-- <img width="120" src={org.logo} alt="{org.name} Logo" /> -->
							<div class="card-body ">
								<h5 class="card-title">
									{org.name}
									{#if org.is_nsfw == true}
										(NSFW)
									{/if}
								</h5>
							</div>
						</div>
						<ul class="list-group list-group-flush">
							<li class="list-group-item">
								<a href={org.merch_url} class="link-dark">
									Official Merch Site <Icon name="box-arrow-up-right" />
								</a>
							</li>
							<li class="list-group-item">
								<a href={org.official_url} class="link-dark">
									Website <Icon name="box-arrow-up-right" />
								</a>
							</li>
						</ul>
					</div>
				</div>
				<!-- <div>
					<div>Tags:</div>
					{#each org.tagmap as tags}
						{tags.tag.name}
					{/each}
				</div> -->
			{/each}
		</div>
	</div>
	<!-- <pre>{JSON.stringify(response, null, 2)}</pre> -->
{/await}
