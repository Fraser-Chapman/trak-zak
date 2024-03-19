<script lang="ts">
	import { ProgressBar } from '@skeletonlabs/skeleton';
	import { differenceInCalendarDays } from 'date-fns';
	import zakRunning from '$lib/assets/zak-running.gif'
	import coastalCliffs from '$lib/assets/coastal-cliff.png'

	const startDate: Date = new Date(2024, 2, 13);
	const endDate: Date = new Date(2024, 3, 11)

	const daysLeftToGo = differenceInCalendarDays(endDate, Date.now())
	const maxProgress = differenceInCalendarDays(endDate, startDate) + 1
	const progress = maxProgress - daysLeftToGo
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center w-full m-5 flex flex-col items-center">
		<h2 class="h2">Trak Zak</h2>

		<div class="flex flex-row justify-between">
			<img class="slide-in" style="margin-left: {((progress / maxProgress) * 100) - 6}%" src="{zakRunning}" alt="Animation of a man walking" width="15%" height="15%" />
			<img src="{coastalCliffs}" alt="" width="15%" height="15%" />
		</div>

		<ProgressBar label="Progress Bar" min={0} value={progress} max={maxProgress} />
		<h3>{daysLeftToGo} Days to go</h3>
	</div>
</div>

<style>
    .slide-in {
        position: relative;
        left: -100%; /* Off-screen initially */
        animation: slideIn 2s forwards; /* Animation duration and direction */
    }

    @keyframes slideIn {
        to {
            left: 0; /* Slide to the left edge */
        }
    }
</style>
