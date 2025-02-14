<script lang="ts">
	import '@fontsource/space-mono/700.css';
	import '../app.css';
</script>

<svelte:head>
	<title>Frontend Mentor | Tip Calculator</title>
</svelte:head>

<header>
	<img src="/images/logo.svg" alt="Splitter App" />
</header>
<main>
	<div class="grid max-w-[920px] gap-8 rounded-t-3xl bg-white p-8 md:grid-cols-2 md:rounded-b-3xl">
		<form class="grid gap-8">
			<div class="grid">
				<label for="bill">Bill</label>
				<div class="relative mt-2">
					<img
						src="/images/icon-dollar.svg"
						alt=""
						class="absolute top-1/2 left-4 -translate-y-1/2"
					/>
					<input
						id="bill"
						type="number"
						class="bg-verylightgrayishcyan focus-visible:outline-strongcyan appearance-textfield text-verydarkcyan caret-strongcyan block w-full rounded-[5px] py-1.5 pr-4 pl-10 text-right text-2xl focus-visible:outline-2"
						placeholder="0"
						min="0"
					/>
				</div>
			</div>
			<div>
				<p>Select Tip %</p>
				<div class="mt-4 grid grid-cols-2 gap-4 md:grid-cols-3 md:gap-x-3.5">
					<div class="group relative">
						<input id="tip-5" class="absolute appearance-none" type="radio" name="tip" value="5" />
						<label
							for="tip-5"
							class="bg-verydarkcyan hover:bg-lightstrongcyan hover:text-verydarkcyan group-has-checked:bg-strongcyan group-has-checked:text-verydarkcyan block cursor-pointer rounded-[5px] p-2 text-center text-2xl text-white transition-colors duration-300 ease-in-out"
						>
							5%
						</label>
					</div>
					<div class="group relative">
						<input
							id="tip-10"
							class="absolute appearance-none"
							type="radio"
							name="tip"
							value="10"
						/>
						<label
							for="tip-10"
							class="bg-verydarkcyan hover:bg-lightstrongcyan hover:text-verydarkcyan group-has-checked:bg-strongcyan group-has-checked:text-verydarkcyan block cursor-pointer rounded-[5px] p-2 text-center text-2xl text-white transition-colors duration-300 ease-in-out"
						>
							10%
						</label>
					</div>
					<div class="group relative">
						<input
							id="tip-15"
							class="absolute appearance-none"
							type="radio"
							name="tip"
							value="15"
						/>
						<label
							for="tip-15"
							class="bg-verydarkcyan hover:bg-lightstrongcyan hover:text-verydarkcyan group-has-checked:bg-strongcyan group-has-checked:text-verydarkcyan block cursor-pointer rounded-[5px] p-2 text-center text-2xl text-white transition-colors duration-300 ease-in-out"
						>
							15%
						</label>
					</div>
					<div class="group relative">
						<input
							id="tip-25"
							class="absolute appearance-none"
							type="radio"
							name="tip"
							value="25"
						/>
						<label
							for="tip-25"
							class="bg-verydarkcyan hover:bg-lightstrongcyan hover:text-verydarkcyan group-has-checked:bg-strongcyan group-has-checked:text-verydarkcyan block cursor-pointer rounded-[5px] p-2 text-center text-2xl text-white transition-colors duration-300 ease-in-out"
						>
							25%
						</label>
					</div>
					<div class="group relative">
						<input
							id="tip-50"
							class="absolute appearance-none"
							type="radio"
							name="tip"
							value="50"
						/>
						<label
							for="tip-50"
							class="bg-verydarkcyan hover:bg-lightstrongcyan hover:text-verydarkcyan group-has-checked:bg-strongcyan group-has-checked:text-verydarkcyan block cursor-pointer rounded-[5px] p-2 text-center text-2xl text-white transition-colors duration-300 ease-in-out"
						>
							50%
						</label>
					</div>
					<div>
						<input
							type="number"
							class="appearance-textfield bg-verylightgrayishcyan text-verydarkcyan caret-strongcyan focus-visible:border-strongcyan size-full rounded-[5px] px-4 text-right text-2xl placeholder:text-center focus-visible:border-2 focus-visible:outline-none"
							placeholder="Custom"
							min="0"
						/>
					</div>
				</div>
			</div>
			<div>
				<label for="people">Number of People</label>
				<div class="relative mt-2">
					<img
						src="/images/icon-person.svg"
						alt=""
						class="absolute top-1/2 left-4 -translate-y-1/2"
					/>
					<input
						id="people"
						type="number"
						class="bg-verylightgrayishcyan focus-visible:outline-strongcyan appearance-textfield text-verydarkcyan caret-strongcyan block w-full rounded-[5px] py-1.5 pr-4 pl-10 text-right text-2xl focus-visible:outline-2"
						placeholder="0"
					/>
				</div>
			</div>
		</form>
		<div
			class="bg-verydarkcyan flex flex-col justify-between rounded-2xl p-6 pt-10 md:px-10 md:py-14"
		>
			<div class="space-y-6">
				<div class="flex items-center justify-between">
					<div>
						<p class="text-white">Tip Amount</p>
						<p class="text-grayishcyan text-sm">/ person</p>
					</div>
					<output class="text-strongcyan text-3xl md:text-5xl">$0.00</output>
				</div>
				<div class="flex items-center justify-between">
					<div>
						<p class="text-white">Total</p>
						<p class="text-grayishcyan text-sm">/ person</p>
					</div>
					<output class="text-strongcyan text-3xl md:text-5xl">$0.00</output>
				</div>
			</div>
			<button
				class="bg-strongcyan text-verydarkcyan hover:bg-lightstrongcyan focus:bg-strongcyan mt-9 cursor-pointer rounded-[5px] py-2 text-xl uppercase transition-colors duration-300 ease-in-out"
			>
				Reset
			</button>
		</div>
	</div>
</main>
