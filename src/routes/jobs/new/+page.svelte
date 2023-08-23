<script>
	import { PUBLIC_BACKEND_BASE_URL } from '$env/static/public';
	import { goto } from '$app/navigation';
	import { getUserId } from '../../../utils/auth';

	let formErrors = {};

	function jobsNew() {
		goto(`/`);
	}

	async function createJob(evt) {
		evt.preventDefault();

		const jobData = {
			user: getUserId(),
			title: evt.target['title'].value,
			minAnnualCompensation: evt.target['minAnnualCompensation'].value,
			maxAnnualCompensation: evt.target['maxAnnualCompensation'].value,
			employer: evt.target['employer'].value,
			location: evt.target['location'].value,
			description: evt.target['description'].value,
			requirements: evt.target['requirements'].value,
			applicationInstructions: evt.target['applicationInstructions'].value
		};

		const resp = await fetch(PUBLIC_BACKEND_BASE_URL + '/api/collections/jobs/records', {
			method: 'POST',
			mode: 'cors',
			headers: {
				'Content-Type': 'application/json'
			},
			body: JSON.stringify(jobData)
		});

		if (resp.status == 200) {
			console.log('success');
			jobsNew();
		} else {
			console.log('fail');
			const res = await resp.json();
			formErrors = res.data;
		}
	}
</script>

<h1 class="text-center text-xl">Post a Job</h1>

<div class="flex justify-center items-center mt-8">
	<form on:submit={createJob} class="w-1/3">
		<div class="form-control w-full">
			<label class="label" for="Title">
				<span class="label-text">Job Title</span>
			</label>
			<input type="title" name="title" class="input input-bordered w-full" required />
			{#if 'title' in formErrors}
				<label class="label" for="title">
					<span class="label-text-alt text-red-500">{formErrors['title'].message}</span>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="minAnnualCompensation">
				<span class="label-text">Min Annual Compensation</span>
			</label>
			<input
				type="minAnnualCompensation"
				name="minAnnualCompensation"
				placeholder=""
				class="input input-bordered w-full"
				required
			/>
			{#if 'minAnnualCompensation' in formErrors}
				<label class="label" for="minAnnualCompensation">
					<span class="label-text-alt text-red-500"
						>{formErrors['minAnnualCompensation'].message}</span
					>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="maxAnnualCompensation">
				<span class="label-text">Max Annual Compensation</span>
			</label>
			<input
				type="maxAnnualCompensation"
				name="maxAnnualCompensation"
				placeholder=""
				class="input input-bordered w-full"
				required
			/>
			{#if 'maxAnnualCompensation' in formErrors}
				<label class="label" for="maxAnnualCompensation">
					<span class="label-text-alt text-red-500"
						>{formErrors['maxAnnualCompensation'].message}</span
					>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="employer">
				<span class="label-text">Employer Name</span>
			</label>
			<input
				type="employer"
				name="employer"
				placeholder=""
				class="input input-bordered w-full"
				required
			/>
			{#if 'employer' in formErrors}
				<label class="label" for="employer">
					<span class="label-text-alt text-red-500">{formErrors['employer'].message}</span>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="location">
				<span class="label-text">Location</span>
			</label>
			<input
				type="location"
				name="location"
				placeholder=""
				class="input input-bordered w-full"
				required
			/>
			{#if 'location' in formErrors}
				<label class="label" for="location">
					<span class="label-text-alt text-red-500">{formErrors['location'].message}</span>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="description">
				<span class="label-text">Description</span>
			</label>
			<textarea
				type="description"
				name="description"
				placeholder=""
				class="textarea textarea-bordered h-40"
				required
			/>
			{#if 'description' in formErrors}
				<label class="label" for="description">
					<span class="label-text-alt text-red-500">{formErrors['description'].message}</span>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="requirements">
				<span class="label-text">Requirements</span>
			</label>
			<textarea
				type="requirements"
				name="requirements"
				placeholder=""
				class="textarea textarea-bordered h-40"
				required
			/>
			{#if 'requirements' in formErrors}
				<label class="label" for="requirements">
					<span class="label-text-alt text-red-500">{formErrors['requirements'].message}</span>
				</label>
			{/if}
		</div>

		<div class="form-control w-full">
			<label class="label" for="applicationInstructions">
				<span class="label-text">Application Instructions</span>
			</label>
			<textarea
				type="applicationInstructions"
				name="applicationInstructions"
				placeholder=""
				class="textarea textarea-bordered h-40"
				required
			/>
			{#if 'applicationInstructions' in formErrors}
				<label class="label" for="applicationInstructions">
					<span class="label-text-alt text-red-500"
						>{formErrors['applicationInstructions'].message}</span>
				</label>
			{/if}
		</div>

		<div class="form-control w-full mt-4">
			<button class="btn btn-md">Post Job</button>
		</div>
	</form>
</div>
