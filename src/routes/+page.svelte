<div class="container mt-5">
	<div class="row justify-content-center">
		<div class="col-md-8">
			<div class="card">
				<div class="card-header">
					<h1 class="card-title mb-0">
						<i class="bi bi-heart-fill text-danger me-2"></i>
						Welcome to SvelteKit
					</h1>
				</div>
				<div class="card-body">
					<p class="card-text">
						Visit <a href="https://svelte.dev/docs/kit" class="btn btn-primary btn-sm">
							<i class="bi bi-book me-1"></i>SvelteKit Documentation
						</a> to read the documentation
					</p>
					
					<div class="mt-4">
						<h5>Bootstrap Components Test</h5>
						<div class="row">
							<div class="col-md-6">
								<div class="alert alert-success" role="alert">
									<i class="bi bi-check-circle me-2"></i>
									Bootstrap CSS is working!
								</div>
							</div>
							<div class="col-md-6">
								<div class="alert alert-info" role="alert">
									<i class="bi bi-info-circle me-2"></i>
									Bootstrap Icons are working!
								</div>
							</div>
						</div>
						
						<div class="mt-3">
							<button type="button" class="btn btn-outline-primary me-2">
								<i class="bi bi-star me-1"></i>Primary
							</button>
							<button type="button" class="btn btn-outline-secondary me-2">
								<i class="bi bi-gear me-1"></i>Secondary
							</button>
							<button type="button" class="btn btn-outline-success">
								<i class="bi bi-check me-1"></i>Success
							</button>
						</div>
					</div>

					<!-- Bootstrap JavaScript Components Test -->
					<div class="mt-5">
						<h5>Bootstrap JavaScript Components</h5>
						
						<!-- Modal Example -->
						<button type="button" class="btn btn-primary me-2" data-bs-toggle="modal" data-bs-target="#exampleModal">
							<i class="bi bi-window me-1"></i>Open Modal
						</button>

						<!-- Dropdown Example -->
						<div class="dropdown d-inline-block me-2">
							<button class="btn btn-secondary dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false">
								<i class="bi bi-list me-1"></i>Dropdown
							</button>
							<ul class="dropdown-menu">
								<li><a class="dropdown-item" href="#"><i class="bi bi-house me-2"></i>Home</a></li>
								<li><a class="dropdown-item" href="#"><i class="bi bi-person me-2"></i>Profile</a></li>
								<li><a class="dropdown-item" href="#"><i class="bi bi-gear me-2"></i>Settings</a></li>
								<li><hr class="dropdown-divider"></li>
								<li><a class="dropdown-item" href="#"><i class="bi bi-box-arrow-right me-2"></i>Logout</a></li>
							</ul>
						</div>

						<!-- Tooltip Example -->
						<button type="button" class="btn btn-info me-2" data-bs-toggle="tooltip" data-bs-placement="top" title="This is a tooltip!">
							<i class="bi bi-question-circle me-1"></i>Hover for Tooltip
						</button>

						<!-- Collapse Example -->
						<button class="btn btn-warning" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
							<i class="bi bi-chevron-down me-1"></i>Toggle Collapse
						</button>
						
						<div class="collapse mt-3" id="collapseExample">
							<div class="card card-body">
								<i class="bi bi-lightbulb me-2"></i>
								This content can be toggled with the button above! Bootstrap JavaScript is working perfectly.
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>

<!-- Modal -->
<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
	<div class="modal-dialog">
		<div class="modal-content">
			<div class="modal-header">
				<h1 class="modal-title fs-5" id="exampleModalLabel">
					<i class="bi bi-window me-2"></i>Bootstrap Modal
				</h1>
				<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
			</div>
			<div class="modal-body">
				<p><i class="bi bi-check-circle-fill text-success me-2"></i>Bootstrap JavaScript is working!</p>
				<p>This modal demonstrates that Bootstrap's JavaScript library is properly loaded and functional.</p>
			</div>
			<div class="modal-footer">
				<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
				<button type="button" class="btn btn-primary">Save changes</button>
			</div>
		</div>
	</div>
</div>

<script>
	import { onMount } from 'svelte';
	
	onMount(() => {
		// Initialize Bootstrap tooltips
		const tooltipTriggerList = document.querySelectorAll('[data-bs-toggle="tooltip"]');
		const tooltipList = [...tooltipTriggerList].map(tooltipTriggerEl => new bootstrap.Tooltip(tooltipTriggerEl));
		
		return () => {
			// Cleanup tooltips on component destroy
			tooltipList.forEach(tooltip => tooltip.dispose());
		};
	});
</script>
