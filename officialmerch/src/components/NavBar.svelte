<script lang="ts">
	import {
		Collapse,
		Navbar,
		NavbarToggler,
		NavbarBrand,
		Nav,
		NavItem,
		NavLink,
		Dropdown,
		DropdownToggle,
		DropdownMenu,
		Spinner
	} from 'sveltestrap';


	let isOpen = false;

	function handleUpdate(event) {
		isOpen = event.detail.isOpen;
	}
	import supabase from '$lib/db';

	async function getCategories() {
		const categories = await supabase.from('category').select(`name`);
		return categories;
	}
</script>

<!-- <Nav class="navbar navbar-expand-lg navbar-dark bg-dark">
	<div class="container-fluid">
		<a class="navbar-brand" href="/">OfficialMer.ch</a>
		<NavbarToggler ontoggle={() => (isOpenNav = !isOpenNav)} />
		<Collapse {isOpen} navbar expand="md" ontoggle={() => (isOpenNav = !isOpenNav)} on:update={handleUpdate}>
			<ul class="navbar-nav me-auto">
				<li class="nav-item">
					<a class="nav-link" href="/">Home </a>
				</li>
				<li class="nav-item">
					<a class="nav-link" href="/about">About</a>
				</li>
				<Dropdown nav {isOpen} toggle={() => (isOpen = !isOpen)}>
					<DropdownToggle nav caret>Categories</DropdownToggle>
					<DropdownMenu class="border-dark">
						{#await getCategories()}
							<Spinner class="dark" />
						{:then response}
							{#each response.data as cat}
								<a class="dropdown-item" href="/{cat.name}">{cat.name}</a>
							{/each}
						{/await}
						<a class="dropdown-item" href="/tech">Tech</a>
						<a class="dropdown-item" href="/retail">Retail</a>
						<a class="dropdown-item" href="/">Other</a>
					</DropdownMenu>
				</Dropdown>
			</ul>
		</Collapse>
	</div>
</Nav> -->

<Navbar color="dark" dark expand="md">
	<NavbarBrand href="/">OfficialMer.ch</NavbarBrand>
	<NavbarToggler on:click={() => (isOpen = !isOpen)} />
	<Collapse {isOpen} navbar expand="md" on:update={handleUpdate}>
		<Nav class="navbar-nav me-auto" navbar>
			<NavItem>
				<NavLink href="/">Home</NavLink>
			</NavItem>
			<NavItem>
				<NavLink href="https://github.com/bestguy/sveltestrap">GitHub</NavLink>
			</NavItem>
			<Dropdown nav inNavbar>
				<DropdownToggle nav caret>Categories</DropdownToggle>
				<DropdownMenu end>
					{#await getCategories()}
						<Spinner class="dark" />
					{:then response}
						{#each response.data as cat}
							<a class="dropdown-item" href="/category/{cat.name.toLowerCase()}">{cat.name}</a>
						{/each}
					{/await}
				</DropdownMenu>
			</Dropdown>
		</Nav>
	</Collapse>
</Navbar>

