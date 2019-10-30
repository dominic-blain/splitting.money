<script>
	import InputText from '../components/forms/InputText.svelte';
	import ButtonMain from '../components/buttons/ButtonMain.svelte';
	let names = [];
	let placeholders = "What's your name?";
	let namePlaceholders = [
		"What's your name?",
		"Add a friend",
		"Add another friend",
		"Add another friend",
		"Add (yet) another friend",
		"What, another one?"
	]
	let newNameValue = "";
	let newNameInputElement;

	$: isGroup = names.length > 1;

	let updateNames = (index, value) => {
		if (value === '') {
			names.splice(index, 1);
			names = names;
		} else if (index > names.length && value !== '') {
			names = [...names, value];
			newNameInputElement.focus();
		}
		newNameValue = '';
	}
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

	.button-ctn {
		text-align: center;
		opacity: 0;
	}

	.button-ctn.isVisible {
		opacity: 1;
	}
	
	.button-ctn span {
		display: block;
		font-size: 18px;
		margin-bottom: 30px;
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
	{#each names as name, index}
		<InputText bind:value={name} handleUpdate={updateNames} {index}  />
	{/each}
	<InputText bind:value={newNameValue} handleUpdate={updateNames} index={names.length + 1} placeholder={namePlaceholders.length > names.length ? namePlaceholders[names.length] : namePlaceholders[1]} bind:inputElement={newNameInputElement}/>
	<div class="button-ctn" class:isVisible={isGroup}>
		<span>OR</span>
		<ButtonMain label="Start $plitting" url="" />
	</div>
</main>
