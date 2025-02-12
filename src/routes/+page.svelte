<script lang="ts">
	import { Line } from 'svelte-chartjs';
	import { Pie } from 'svelte-chartjs';
	import { data } from '$lib/data.js';

	import {
		Chart as ChartJS,
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		PointElement,
		ArcElement,
		CategoryScale
	} from 'chart.js';

	ChartJS.register(
		Title,
		Tooltip,
		Legend,
		LineElement,
		LinearScale,
		ArcElement,
		PointElement,
		CategoryScale
	);
	type ChartData = {
		labels: (string | number)[];
		datasets: {
			label: string;
			fill: boolean;
			borderColor: string;
			data: number[];
			backgroundColor?: string[];
			hoverBackgroundColor?: string[];
		}[];
	};

	let year: number = 2023;

	let chart1: ChartData = {
		labels: data.map((element) => element.year),
		datasets: [
			{
				label: 'male',
				fill: false,
				borderColor: 'rgb(54, 162, 235)',
				data: data.map((element) => element.m)
			},
			{
				label: 'female',
				fill: false,
				borderColor: 'rgb(255, 99, 132)',
				data: data.map((element) => element.f)
			}
		]
	};

	let chart2: ChartData = {
		labels: ['m', 'f'],
		datasets: [
			{
				data: [12, 23],

				backgroundColor: ['rgb(124,12,124)', 'rgb(12,12,12)']
			}
		]
	};
	console.log(data.map((element) => [element.year]));
</script>

<div class="container mx-auto">
	<div class="grid grid-cols-2 gap-10 mb-10">
		<div class="border-4 border-violet-200 p-3">
			<h2 class="text-center text-2xl text-violet-700 font-bold">Graf podatkov</h2>
			<Line data={chart1} options={{ responsive: true }} />
		</div>
		<div class="border-4 border-violet-200 p-3">
			<h2 class="text-center text-2xl text-violet-700 font-bold">Graf podatkov</h2>
			<input class="border border-black w-full text-center" type="numbe" bind:value={year} />
			<Pie data={chart2} options={{ responsive: true }} />
		</div>
	</div>
</div>

{#each data as year}
	<p>{year.year} rojenih: {year.f} deklet in {year.m} fantov</p>
{/each}
