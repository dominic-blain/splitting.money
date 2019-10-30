<script>
    import { onMount } from 'svelte';

    export let index;
    export let placeholder = '';
    export let value;
    export let handleUpdate;
    export let inputElement = '';
    
    let element;
    let isFocused = false;

    $: isFilled = value.length != 0;
    $: isCompleted = isFilled && !isFocused;

    let handleKeydown = (event) => {
        if (event.key === 'Enter' && isFilled) {
            handleUpdate(index, value);
        }
    }

    let handleFocus = () => {
        isFocused = true;
    }

    let handleBlur = () => {
        isFocused = false;
        handleUpdate(index, value);
    }

    onMount(() => {
        inputElement = element;
    });

</script>

<style>
.ctn {
    position: relative;
    width: 100%;
    margin-bottom: 10px;
    transition: margin 90ms ease-out;
}

.ctn:not(.isCompleted) {
    margin-bottom: 40px;
}

input {
    display: block;
    width: 100%;
    height: 50px;
    padding: 5px 20px;
    box-sizing: border-box;
    border: 2px solid var(--green-100);
    font-size: 16px;
    font-family: var(--font-main);
    color: var(--black-100);
    background-color: white;
    position: relative;
    z-index: 1;
    outline: none;

    transition: 90ms ease-out;
    transition-property: border-color, background-color;
}

.ctn.isCompleted input {
    border-color: var(--green-10);
    background-color: var(--green-10);
}

.ctn.isCompleted .shadow {
    opacity: 0;
}

::placeholder {
    color: var(--grey-100);
}

.shadow {
    position: absolute;
    top: 50%;
    left: 20px;
    right: 20px;
    bottom: 0px;
    box-shadow: 0px 4px 16px var(--green-100);
    opacity: 0.5;

    transition: opacity 90ms ease-out;
}

.button-enter {
    position: absolute;
    top: 100%;
    margin-top: 5px;
    opacity: 0;
    visibility: hidden;
    transform: translateY(-25%);
    transition: opacity 45ms ease-out, transform 45ms ease-out, visibility 0ms 45ms;
}
/* ~> IS VISIBLE */
.ctn:not(.isCompleted) .button-enter.isVisible {
    opacity: 1;
    visibility: visible;
    transform: translateY(0%);
    transition-delay: 0ms;
}
</style>

<svelte:window on:keydown={handleKeydown} />

<div class="ctn" class:isCompleted>
    <div class="shadow"></div>
    <input placeholder={placeholder} bind:value={value} on:focus={handleFocus} on:blur={handleBlur} bind:this={element} />
    <div class="button-enter" class:isVisible={isFilled} on:click={handleUpdate}>Press enter</div>
</div>