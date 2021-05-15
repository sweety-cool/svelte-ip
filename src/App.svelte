<script>
	import { InlineLoading, Tile, Row, Column } from "carbon-components-svelte";
	import WirelessModem from "carbon-pictograms-svelte/lib/WirelessModem.svelte";

	const url = "http://ip-api.com/json/?fields=21757951";

	let DATA;
	fetch(url)
		.then((r) => r.json())
		.then((data) => (DATA = data));
</script>

<div class="container">
	<br />
	<h1 class="center">IP Info</h1>
	<p class="center">by Sweety</p>
	<br />
	<br />

	{#if DATA}
		<Tile class="center">
			<WirelessModem />
			<br /><br />
			<h2>{DATA.query}</h2>
		</Tile>
		<br />

		<Tile class="center">
			<h3>{DATA.isp}</h3>
		</Tile>

		<br />

		<Row>
			<Column>
				<Tile>
					<h3>Geolocation</h3>
					<p>Country: {DATA.country}</p>
					<p>Region: {DATA.regionName}</p>
					<p>City: {DATA.city}</p>
					<p>PIN: {DATA.zip}</p>
				</Tile>
			</Column>
			<Column>
				<iframe
					src="https://maps.google.com/maps?q={DATA.lat},{DATA.lon}&output=embed"
					title="map"
				/>
			</Column>
		</Row>

		<br />

		<Tile>
			<p>Time Zone: {DATA.timezone}</p>
			<p>AS Name: {DATA.asname}</p>
		</Tile>
	{:else}
		<InlineLoading />
	{/if}
</div>

<style>
</style>
