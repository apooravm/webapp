<script lang="ts">
	import type { PageData } from '../$types';
	import type { Note, NoteInfoResponse } from '$lib/utils';

	const cleanTime = (timeStr: string) => {
		let parts = timeStr.split(':');
		return `${parts[0]}:${parts[1]}`;
	};

	export let data: PageData;
</script>

<div class="main-container">
	{#await JSON.parse(data.message)}
		<div class="loader" />
	{:then data}
		{#each data.notes as { title, description, slug, date, time }}
			<div class="note-container">
				<div class="note-title">
					{title}
				</div>
				<div class="note-datetime">
					{cleanTime(time)}, {date}
				</div>
				<br />
				<div class="note-desc">
					{description}
				</div>
				<a class="note-link" href={`https://multi-serve.onrender.com/api/notes/${slug}.md`}>Link Here</a>
			</div>
		{/each}
	{/await}
</div>

<!-- 

vim.opt.backspace = '2'
vim.opt.showcmd = true
vim.opt.laststatus = 2
vim.opt.autowrite = true
vim.opt.autoread = true

 -->

<style>
	.main-container {
		display: flex;
		flex-direction: column;
		justify-content: space-evenly;
	}

	.note-container {
		display: flex;
		flex-direction: column;
		justify-content: center;

		font-family: monospace;

		background-color: white;
		border: 1px solid #ccc;
		border-radius: 8px;
		box-shadow: 0 0 0px rgba(0, 0, 0, 0.1);
		/* border: 0.1px transparent solid; */
		/* margin: 20px; */
	}

	.note-desc {
		font-size: 90%;
		font-weight: lighter;
	}

	.note-datetime {
		font-weight: lighter;
		font-size: 80%;
	}

	.note-link {
		font-weight: lighter;
		text-decoration: none;
	}

	.note-container:hover {
		cursor: pointer;

		background: none;

		background-color: rgb(235, 235, 235);

		transition: all 0.1s;
		/* border: 0.1px rgba(42, 42, 42, 0.223) solid; */
	}

	@-webkit-keyframes spin {
		0% {
			-webkit-transform: rotate(0deg);
		}
		100% {
			-webkit-transform: rotate(360deg);
		}
	}

	@keyframes spin {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}

	@media only screen and (min-width: 600px) {
		.main-container {
			padding-block: 50px;

			padding-inline: 200px;
			margin: auto;

			gap: 50px;
		}

		.note-container {
			max-height: 40rem;
			max-width: 50rem;

			padding-block: 35px;
			padding-inline: 40px;

			font-size: 100%;

			transition: all 0.6s;
		}

		.note-title {
			font-size: 140%;
			font-weight: 900;
		}

		.note-link {
			font-size: 90%;
		}
	}

	@media only screen and (max-width: 600px) {
		.main-container {
			display: flex;
			flex-direction: column;
			gap: 10px;
			justify-content: center;
			align-items: center;

			margin-block: 15px;
			margin-inline: 10px;
		}

		.note-container {
			min-height: 14rem;

			font-size: 100%;
			padding-inline: 20px;
		}

		.note-title {
			font-size: 110%;
			font-weight: 900;
		}

		.note-link {
			font-size: 80%;
		}
	}
</style>
