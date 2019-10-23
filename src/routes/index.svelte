<script>
	import InputText from '../components/forms/InputText.svelte';
	let people = [];
</script>

<style>
	header {
		display: flex;
		flex-direction: column;
		justify-content: flex-end;
		align-items: center;
		min-height: 50vh;
		padding-bottom: 8vh;
		box-sizing: border-box;
		text-align: center;
	}
	h1 {
		display: none;
	}
	h2 {
		font-size: 18px;
		font-weight: 400;
	}

	main {
		min-height: 50vh;
		padding: 0 3vw;
		max-width: 400px;
		margin: 0 auto;
	}
</style>

<svelte:head>
	<title>$plitting | Money with Friends</title>
</svelte:head>




<header>
	<h1>$plitting</h1>
	<div class="logo">
		<img src="logo-splitting.svg" alt="splitting logo" />
	</div>
	<h2>Easiest way to<br/>split money with friends</h2>
</header>

<main>
	<InputText />
</main>
