<script lang="ts">
	import '@fontsource/space-mono/700.css';
	import '../app.css';
</script>

<svelte:head>
	<title>Frontend Mentor | Tip Calculator</title>
</svelte:head>

<div>
	<header>
		<img src="/images/logo.svg" alt="Splitter App" />
	</header>
	<main>
		<div>
			<form>
				<div>
					<label for="bill">Bill</label>
					<input id="bill" type="number" />
				</div>
				<div>
					<p>Select Tip %</p>
					<div>
						<div>
							<input />
							<label>5%</label>
						</div>
						<div>
							<input />
							<label>10%</label>
						</div>
						<div>
							<input />
							<label>15%</label>
						</div>
						<div>
							<input />
							<label>25%</label>
						</div>
						<div>
							<input />
							<label>50%</label>
						</div>
						<div>
							<input />
						</div>
					</div>
				</div>
				<div>
					<label for="people">Number of People</label>
					<input id="people" type="number" />
				</div>
			</form>
			<div>
				<div>
					<div>
						<div>
							<p>Tip Amount</p>
							<p>/ person</p>
						</div>
						<output>$0.00</output>
					</div>
					<div>
						<div>
							<p>Total</p>
							<p>/ person</p>
						</div>
						<output>$0.00</output>
					</div>
				</div>
				<button>Reset</button>
			</div>
		</div>
	</main>
</div>
