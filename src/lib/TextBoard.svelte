<script>

	import { onMount } from "svelte";
    import Counter from "./Counter.svelte";
	let testCharacters = [
	  'w', 'h', 'e', 'n', ' ', 'b', 'y', ' ', 's', 'i', 'n', 'c', 'e', ' ', 'l', 'a', 't', 'e', ' ', 'a', 'n', 'o', 't', 'h', 'e', 'r', 
	  ' ', 'e', 'a', 'r', 'l', 'y', ' ', 'o', 'w', 'n', ' ', 'u', 's', 'e', ' ', 's', 'h', 'o', 'u', 'l', 'd', ' ', 'f', 'r', 'o', 'm', 
	  ' ', 'i', 'n', ' ', 'w', 'i', 't', 'h', 'o', 'u', 't', ' ', 's', 'h', 'e', ' ', 'i', 'n', 't', 'o', ' ', 'a', 'g', 'a', 'i', 'n', 
	  's', 't', ' ', 'f', 'a', 'c', 'e', ' ', 'l', 'e', 'a', 'v', 'e', ' ', 'a', 'l', 's', 'o', ' ', 'h', 'o', 'm', 'e', ' ', 'l', 'o', 
	  'n', 'g', ' ', 'c', 'h', 'a', 'n', 'g', 'e', ' ', 'a', 'l', 'l', ' ', 'b', 'e', ' ', 's', 'o', ' ', 'p', 'e', 'o', 'p', 'l', 'e', 
	  ' ', 'f', 'i', 'n', 'd', ' ', 'n', 'o', ' ', 'p', 'e', 'r', 's', 'o', 'n', ' ', 'b', 'e', ' ', 'l', 'o', 'n', 'g', ' ', 'm', 'e', 
	  'a', 'n', ' ', 'p', 'u', 'b', 'l', 'i', 'c', ' ', 'w', 'h', 'a', 't', ' ', 't', 'h', 'e', 'r', 'e', ' ', 'a', 'l', 's', 'o', 
	  ' ', 'i', 'n', ' ', 'l', 'i', 't', 't', 'l', 'e'
	];
	let inputCharacters = [];
	let input;
	let cursor;

	onMount(() => {
		let cursorPositionedElement = document.querySelectorAll("span")[inputCharacters.length];
		const rect = cursorPositionedElement.getBoundingClientRect();
		cursor.style.left = `${rect.left + 1}px`
		cursor.style.top = `${rect.top + 6}px`
		input.focus()
	})

	function handleInput(e) {
		inputCharacters = e.target.value.split("")

		let cursorPositionedElement = document.querySelectorAll("span")[inputCharacters.length - 1];
		const rect = cursorPositionedElement.getBoundingClientRect();
		cursor.style.left = `${rect.right + 1}px`
		cursor.style.top = `${rect.top + 6}px`


		cursorPositionedElement.style.opacity = 1
		console.log(cursorPositionedElement)
	}


</script>

<div class="text-board-container">
	<div class="text-container">
		{#each testCharacters as char}
		 	<span>{char}</span>
		{/each}
		<div bind:this={cursor} class="cursor"></div>
	</div>
	<input class="input" type="text" on:input={handleInput} bind:this={input} />
</div>

<style>
	.text-board-container {
		width: 100%;
		display: flex;
		justify-content: center;
	}
	.text-container {
		width: 80%;
		font-size: 2rem;
		text-align: left;
	}	
	.text-container > span {
		opacity: 0.4;
	}
	.input {
		width: 0;
		height: 0;
		opacity: 0;
	}
	.cursor {
		position: absolute;
		height: 2rem;
		width: 2px;
		background-color: orange;

		transition: all 0.25s ease;

		animation-name: breathing;
		animation-duration: 1s;
		animation-iteration-count: infinite;
		animation-fill-mode: forwards;
		animation-timing-function:cubic-bezier(0.86, 0, 0.07, 1);
	}
	
	/* breathing animation for the cursor */
	@keyframes breathing {
		0% {
			opacity: 0;
		}
		50% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}

</style>
