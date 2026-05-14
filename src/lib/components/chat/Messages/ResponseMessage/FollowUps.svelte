<script lang="ts">
	import Tooltip from '$lib/components/common/Tooltip.svelte';
	import { getContext } from 'svelte';
	import ChatPlus from '$lib/components/icons/ChatPlus.svelte';

	const i18n = getContext('i18n');

	export let followUps: string[] = [];
	export let onClick: (followUp: string) => void = () => {};
	export let onOpenInNewChat: (followUp: string) => void = () => {};
</script>

<div class="mt-4">
	<div class="text-sm font-medium">
		{$i18n.t('Follow up')}
	</div>

	<div class="flex flex-col text-left gap-1 mt-1.5">
		{#each followUps as followUp, idx (idx)}
			<div class="flex items-center gap-1">
				<Tooltip content={followUp} placement="top-start" className="line-clamp-1 flex-1">
					<button
						type="button"
						class=" py-1.5 bg-transparent text-left text-sm flex items-center gap-2 text-gray-500 dark:text-gray-400 hover:text-black dark:hover:text-white transition cursor-pointer w-full min-w-0"
						on:click={() => onClick(followUp)}
						aria-label={$i18n.t('Follow up: {{question}}', { question: followUp })}
					>
						<div class="line-clamp-1">
							{followUp}
						</div>
					</button>
				</Tooltip>

				<Tooltip content={$i18n.t('Open in new chat')} placement="top">
					<button
						type="button"
						class="shrink-0 p-1.5 rounded-lg text-gray-400 dark:text-gray-500 hover:text-black dark:hover:text-white hover:bg-black/5 dark:hover:bg-white/5 transition"
						on:click={() => onOpenInNewChat(followUp)}
						aria-label={$i18n.t('Open follow-up in new chat: {{question}}', {
							question: followUp
						})}
					>
						<ChatPlus className="size-4" strokeWidth="2" />
					</button>
				</Tooltip>
			</div>

			{#if idx < followUps.length - 1}
				<hr class="border-gray-50 dark:border-gray-850/30" />
			{/if}
		{/each}
	</div>
</div>
