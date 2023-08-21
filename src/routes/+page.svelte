<script lang="ts">
	const winningCombos = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8],
		[2, 4, 6]
	];

	const gameboard = [
		[0, 0, 0],
		[0, 0, 0],
		[0, 0, 0]
	];

	let currentPlayer = 1;
	let winner = 0;

	const place = (x: number, y: number) => {
		if (winner !== 0) return;
		if (gameboard[y][x] !== 0) return;
		gameboard[y][x] = currentPlayer;
		currentPlayer = currentPlayer === 1 ? 2 : 1;
		checkWin();
	};

	const checkWin = () => {
		for (const combo of winningCombos) {
			const [a, b, c] = combo;
			if (
				gameboard[Math.floor(a / 3)][a % 3] !== 0 &&
				gameboard[Math.floor(a / 3)][a % 3] === gameboard[Math.floor(b / 3)][b % 3] &&
				gameboard[Math.floor(a / 3)][a % 3] === gameboard[Math.floor(c / 3)][c % 3]
			) {
				winner = gameboard[Math.floor(a / 3)][a % 3];
				return;
			}
		}
	};
</script>

<h1 class="text-4xl">embeds tic tac toe</h1>
<h2>
	{#if winner !== 0}
		{winner === 1 ? '❌' : '⭕'} wins!
	{:else}
		current player: {currentPlayer === 1 ? '❌' : '⭕'}
	{/if}
</h2>
<div class="flex flex-col">
	{#each gameboard as row, y}
		<div class="flex flex-row">
			{#each row as cell, x}
				<button
					class="w-16 h-16 border border-black flex justify-center items-center"
					on:click|preventDefault={() => place(x, y)}
				>
					{#if cell === 0}
						&nbsp;
					{:else if cell === 1}
						❌
					{:else if cell === 2}
						⭕
					{/if}
				</button>
			{/each}
		</div>
	{/each}
</div>
