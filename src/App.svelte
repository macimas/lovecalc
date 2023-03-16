<script>
	import Rand, {PRNG} from 'rand-seed';

	let lover1 = '';
	let lover2 = '';
	let percentage, loveText, loveIcon;

	function calculatePercentage() {
		if (!lover1 || !lover2) return alert('please fill all inputs');
		let rand = new Rand((lover1 + lover2).toLowerCase().trim());
		console.log(percentage = Math.round(rand.next() * 101));
		loveText = `<b>${lover1}</b> loves <b>${lover2}</b> this much:`
		switch (true) {
			case percentage < 10: loveIcon = 'broken heart'; break;
			case percentage < 25: loveIcon = 'anatomical heart'; break;
			case percentage < 50: loveIcon = 'beating heart'; break;
			case percentage < 75: loveIcon = 'heart with ribbon'; break;
			case percentage < 100: loveIcon = 'red heart'; break;
			case percentage == 101: loveIcon = 'heart hands'; break;
		}
	}

	function inputEnter(event) {
		if (event.key == 'Enter') calculatePercentage()
	}

	function swapLovers() {
		[lover1, lover2] = [lover2, lover1]
	}
</script>

<main>
	<div>
		<img src="/img/logo.svg"><br>
		<span class="tinted-text">calculate the percentage how much one loves the other!</span>
	</div>

	<div class="lovers">
		<div>
			<input type="text" on:keydown={inputEnter} bind:value={lover1}>
			<button class="heart" title="click me to swap!" on:click={swapLovers}>❤️</button>
			<input type="text" on:keydown={inputEnter} bind:value={lover2}>
		</div>
		<button on:click={calculatePercentage}>calculate!</button>
	</div>

	{#if percentage !== undefined}
		<div class="percentage">
			<span>{@html loveText}</span>
			<h1><img src={`/img/icon/${loveIcon}.png`} height="48">{percentage}%</h1>
			<!--<span>placeholder text</span>-->
		</div>
	{:else}

	{/if}

	<sub class="tinted-text"><i><b>NOTICE:</b> lovecalc <b>DOES NOT</b> provide accurate results when comparing with the real world, even if they seem to be "subjectively or objectively" accurate. lovecalc is not responsible for any breakdown of social interactions, or relationships.</i></sub>

	<sub class="tinted-text">
		<a href="https://macimas.github.io">created by macimas</a> • last updated on March 16, 2023
		<br>
		<a href="https://fonts.google.com/noto/specimen/Noto+Color+Emoji">emojis stolen from Noto Color Emoji</a>
	</sub>
</main>