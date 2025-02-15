<script lang="ts">
	import '@fontsource/space-mono/700.css';
	import { cubicInOut, expoInOut } from 'svelte/easing';
	import { Tween } from 'svelte/motion';
	import '../app.css';

	const tipPresets = [5, 10, 15, 25, 50];

	let billTotal: number | undefined = $state(undefined);
	let tipPercent: number | undefined = $state(undefined);
	let customTipPercent: number | undefined = $state(undefined);
	let people: number | undefined = $state(undefined);

	let tipAmountPerPerson = $derived.by(() => {
		const selectedTip = customTipPercent ?? tipPercent;

		if (!billTotal || !selectedTip || !people) return 0;
		return (billTotal * (selectedTip / 100)) / people;
	});

	let totalPerPerson = $derived.by(() => {
		if (!billTotal || !people || tipAmountPerPerson < 0) return 0;
		return billTotal / people + tipAmountPerPerson;
	});

	const setTip = (percent: number) => {
		customTipPercent = undefined;
		tipPercent = percent;
	};

	const reset = () => {
		billTotal = undefined;
		tipPercent = undefined;
		customTipPercent = undefined;
		people = undefined;
		tweenedTipAmount.set(0);
		tweenedTotal.set(0);
	};

	const tweenedTipAmount = new Tween(0, {
		delay: 200,
		duration: 400,
		easing: expoInOut
	});

	const tweenedTotal = new Tween(0, {
		delay: 400,
		duration: 600,
		easing: cubicInOut
	});

	$effect(() => {
		tweenedTipAmount.set(tipAmountPerPerson);
		tweenedTotal.set(totalPerPerson);
		return () => {
			tweenedTipAmount.set(0);
			tweenedTotal.set(0);
		};
	});
</script>

<svelte:head>
	<title>Frontend Mentor | Tip Calculator</title>
</svelte:head>

<header>
	<img src="/images/logo.svg" alt="Splitter App" />
</header>
<main>
	<div
		class="shadow-card grid max-w-[920px] gap-8 rounded-t-3xl bg-white p-8 md:grid-cols-2 md:gap-12 md:rounded-b-3xl md:p-12 md:pr-8"
	>
		<form class="grid gap-8">
			<div class="grid">
				<label for="bill" class="col-start-1 col-end-1 row-start-1 row-end-1">Bill</label>
				<span class="text-orange col-start-2 col-end-2 row-start-1 row-end-1 ml-auto">
					{#if !billTotal}
						Can't be zero
					{/if}
				</span>
				<div class="relative col-span-2 mt-2">
					<img
						src="/images/icon-dollar.svg"
						alt=""
						class="absolute top-1/2 left-4 -translate-y-1/2"
					/>
					<input
						bind:value={billTotal}
						id="bill"
						type="number"
						name="bill"
						class="bg-verylightgrayishcyan focus-visible:outline-strongcyan appearance-textfield text-verydarkcyan caret-strongcyan invalid:outline-orange block w-full rounded-[5px] py-1.5 pr-4 pl-10 text-right text-2xl invalid:outline-2 focus-visible:outline-2"
						placeholder="0"
						min="1"
						step="0.01"
						required
						aria-invalid={!billTotal || billTotal < 0}
						onchange={(e) => {
							if (e.currentTarget.valueAsNumber < 0) {
								billTotal = 0;
							}
						}}
					/>
				</div>
			</div>
			<div>
				<div class="flex justify-between">
					<p>Select Tip %</p>
					<span class="text-orange">
						{#if (!tipPercent && customTipPercent === undefined) || (customTipPercent && customTipPercent < 0)}
							Select a tip
						{/if}
					</span>
				</div>
				<div class="mt-4 grid grid-cols-2 gap-4 md:grid-cols-3 md:gap-x-3.5">
					{#each tipPresets as tip}
						<div class="group relative">
							<input
								id="tip-{tip}"
								type="radio"
								name="tip"
								value={tip}
								onclick={() => setTip(tip)}
								checked={tip === tipPercent}
								class="peer absolute appearance-none"
							/>
							<label
								for="tip-{tip}"
								class={[
									'group-has-focus:bg-strongcyan! hover:bg-lightstrongcyan hover:text-verydarkcyan block cursor-pointer rounded-[5px] p-2 text-center text-2xl transition-colors duration-300 ease-in-out',
									tip === tipPercent
										? 'bg-strongcyan text-verydarkcyan'
										: 'bg-verydarkcyan text-white'
								]}
							>
								{tip}%
							</label>
						</div>
					{/each}

					<input
						bind:value={customTipPercent}
						type="number"
						name="custom-tip"
						class="appearance-textfield bg-verylightgrayishcyan text-verydarkcyan invalid:border-orange caret-strongcyan focus-visible:border-strongcyan size-full rounded-[5px] px-4 text-right text-2xl placeholder:text-center invalid:border-2 focus-visible:border-2 focus-visible:outline-none"
						placeholder="Custom"
						min="0"
						step="0.01"
						aria-invalid={customTipPercent === undefined && customTipPercent! < 0}
						onfocus={() => {
							if (tipPresets.includes(tipPercent as number)) {
								setTip(0);
							}
						}}
						onchange={(e) => {
							if (e.currentTarget.valueAsNumber < 0) {
								customTipPercent = 0;
							}
						}}
					/>
				</div>
			</div>
			<div class="grid">
				<label for="people" class="col-start-1 col-end-1 row-start-1 row-end-1">
					Number of People
				</label>
				<span class="text-orange col-start-2 col-end-2 row-start-1 row-end-1 ml-auto">
					{#if !people}
						Can't be zero
					{/if}
				</span>
				<div class="relative col-span-2 mt-2">
					<img
						src="/images/icon-person.svg"
						alt=""
						class="absolute top-1/2 left-4 -translate-y-1/2"
					/>
					<input
						bind:value={people}
						id="people"
						type="number"
						name="people"
						class="bg-verylightgrayishcyan focus-visible:outline-strongcyan appearance-textfield text-verydarkcyan caret-strongcyan invalid:outline-orange block w-full rounded-[5px] py-1.5 pr-4 pl-10 text-right text-2xl invalid:outline-2 focus-visible:outline-2"
						placeholder="0"
						min="1"
						required
						aria-invalid={!people || people < 0}
						onchange={(e) => {
							if (e.currentTarget.valueAsNumber < 0) {
								people = 0;
							}
						}}
					/>
				</div>
			</div>
		</form>
		<div
			class="bg-verydarkcyan flex flex-col justify-between rounded-2xl p-6 pt-10 md:px-10 md:pt-14 md:pb-10"
		>
			<div class="space-y-6">
				<div class="flex items-center justify-between">
					<div>
						<p class="text-white">Tip Amount</p>
						<p class="text-grayishcyan text-sm">/ person</p>
					</div>
					<output class="text-strongcyan text-3xl md:text-5xl">
						${tweenedTipAmount.current.toFixed(2)}
					</output>
				</div>
				<div class="flex items-center justify-between">
					<div>
						<p class="text-white">Total</p>
						<p class="text-grayishcyan text-sm">/ person</p>
					</div>
					<output class="text-strongcyan text-3xl md:text-5xl">
						${tweenedTotal.current.toFixed(2)}
					</output>
				</div>
			</div>
			<button
				class="bg-strongcyan text-verydarkcyan hover:bg-lightstrongcyan focus:bg-strongcyan disabled:bg-muteddarkcyan mt-9 cursor-pointer rounded-[5px] py-2 text-xl uppercase transition-colors duration-300 ease-in-out disabled:cursor-not-allowed"
				onclick={() => reset()}
				disabled={!billTotal && !tipPercent && !customTipPercent && !people}
			>
				Reset
			</button>
		</div>
	</div>
</main>
