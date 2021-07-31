<script lang="ts">
	import supabase from '$lib/db';
	import { Icon, Spinner } from 'sveltestrap';
	async function getOrgs() {
		const publicOrgs = await supabase
			.from('organization')
			.select(`name, merch_url, official_url, is_nsfw`)
			.eq('is_public', true);
		return publicOrgs;
	}
</script>

<!-- TODO randomize the order of the organizations and provide a way to order them eventually too -->

{#await getOrgs()}
	<Spinner class="text-primary" style="margin-top: 10rem;" />
{:then response}
	<div class=" p-5">
		<div class="row row-cols-7 gap-3 justify-content-center">
			{#each response.data as org}
				<div class="col ">
					<!-- When adding the logos back use h-100 and a flex or something to make sure the links stick to the bottom and there isnt some ugly chin on the cards -->
					<div class="card bg-light border-dark card-size ">
						<div class="d-flex flex-column align-items-center m-2 ">
							<!-- <img width="120" src={org.logo} alt="{org.name} Logo" /> -->
							<div class="card-body d-flex flex-row">
								<h5 class="card-title">
									{org.name}
								</h5>
								<span class="ms-2">
									{#if org.is_nsfw == true}
										<span class="badge bg-danger">NSFW</span>
									{/if}
								</span>
							</div>
						</div>
						<ul class="list-group list-group-flush">
							<li class="list-group-item">
								<a target="_blank" href={org.merch_url} class="link-primary">
									Official Merch Site <Icon name="box-arrow-up-right" />
								</a>
							</li>
							<li class="list-group-item">
								<a target="_blank" href={org.official_url} class="link-primary">
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

<style>
	a {
		text-decoration: none;
	}

	.card-size {
		min-width: 17rem;
	}

	@media (min-width: 900px) {
		.card-size {
			min-width: 17rem;
			max-width: fit-content;
		}
	}
</style>
