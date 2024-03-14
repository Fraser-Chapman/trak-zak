<script lang="ts">
	import { ProgressBar } from '@skeletonlabs/skeleton';
	import { differenceInCalendarDays } from 'date-fns';

	const startDate: Date = new Date(2024, 2, 13);
	const endDate: Date = new Date(2024, 3, 11)

	const daysLeftToGo = differenceInCalendarDays(endDate, Date.now())
	const maxProgress = differenceInCalendarDays(endDate, startDate) + 1
	const progress = maxProgress - daysLeftToGo
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center flex flex-col items-center">
		<h2 class="h2">Trak Zak</h2>

		<ProgressBar label="Progress Bar" min={0} value={progress} max={maxProgress} />
		<h3>{daysLeftToGo} Days to go</h3>
	</div>
</div>
