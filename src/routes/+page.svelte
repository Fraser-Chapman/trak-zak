<script lang="ts">
	import { ProgressBar } from '@skeletonlabs/skeleton';
	import { differenceInCalendarDays, differenceInMilliseconds } from 'date-fns';
	import confetti from 'canvas-confetti';
	import zakRunning from '$lib/assets/zak-running.gif'
	import coastalCliffs from '$lib/assets/coastal-cliff.png'
	import { browser } from '$app/environment';

	const startDate: Date = new Date(2024, 2, 13);
	const endDate: Date = new Date(2024, 3, 11)

	const millisLeftToGo = differenceInMilliseconds(endDate, Date.now())
	const daysLeftToGo = differenceInCalendarDays(endDate, Date.now()) >= 0 ? differenceInCalendarDays(endDate, Date.now()) : 0
	const maxProgress = differenceInMilliseconds(endDate, startDate) + 1
	const progress = (maxProgress - millisLeftToGo) <= maxProgress ? (maxProgress - millisLeftToGo) : maxProgress

	if (browser && progress >= maxProgress) {
		initiateConfetti()
	}

	function initiateConfetti() {
		const duration = 15 * 1000;
		const animationEnd = Date.now() + duration;
		const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

		function randomInRange(min: number, max: number) {
			return Math.random() * (max - min) + min;
		}

		const interval = setInterval(() => {
			const timeLeft = animationEnd - Date.now();

			if (timeLeft <= 0) {
				return clearInterval(interval);
			}

			const particleCount = 50 * (timeLeft / duration);
			// since particles fall down, start a bit higher than random
			confetti({ ...defaults, particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } });
			confetti({ ...defaults, particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } });
		}, 250);
	}
</script>

<div class="container h-full mx-auto flex justify-center items-center">
	<div class="space-y-10 text-center w-full m-5 flex flex-col items-center">
		<h2 class="h2">Trak Zak</h2>

		<div class="flex flex-row justify-between">
			<img class="slide-in" style="margin-left: {((progress / maxProgress) * 100) - 6}%; margin-right: -{((progress / maxProgress) * 100) - 6}%" src="{zakRunning}" alt="Animation of a man walking" width="15%" height="15%" />
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
