<script>
  import { generateClient } from 'aws-amplify/data';
  import '$lib/amplify';
  import { browser } from '$app/environment';

  const client = generateClient();
  
  let todos = $state([]);
  let channel;
  let isLoading = $state(true);
  let error = $state(null);	
  
  async function loadTodos() {
    try {
      isLoading = true;
      const { data } = await client.models.Todo.list();
      todos = data || [];
    } catch (err) {
      error = err.message;
    } finally {
      isLoading = false;
    }
  }

  // Set up Broadcast Channel for cross-window communication
  $effect(() => {
    if (browser) {
      channel = new BroadcastChannel('todo-updates');
      
      // Listen for updates from other windows
      channel.onmessage = (event) => {
        if (event.data === 'refresh') {
          loadTodos();
        }
      };

      loadTodos(); // Initial load

      return () => channel.close();
    }
  });

  function notifyOtherWindows() {
    if (channel) {
      channel.postMessage('refresh');
    }
  }

  async function createTodo() {
    await client.models.Todo.create({
      content: 'New todo item',
      isDone: false,
    });
    await loadTodos();
    notifyOtherWindows();
  }

  async function updateTodo(id, isDone) {
    await client.models.Todo.update({
      id: id,
      isDone: !isDone,
    });
    await loadTodos();
    notifyOtherWindows();
  }

  async function deleteTodo(id) {
    await client.models.Todo.delete({ id });
    await loadTodos();
    notifyOtherWindows();
  }
</script>



<div class="container mt-5">
	<div class="row justify-content-center">
		<div class="col-md-8">
			<div class="card">
				<div class="card-header">
					<h1 class="card-title mb-0">
						<i class="bi bi-bullseye text-danger me-2"></i>
						AWS Uturn Clients
					</h1>
				</div>
				<div class="card-body">
					<p class="card-text">
						Welcome to your SvelteKit application with Bootstrap integration.
					</p>
					
					<div class="mt-4">
						<h5>Features</h5>
						<div class="row">
							<div class="col-md-6">
								<div class="alert alert-info" role="alert">
									<i class="bi bi-info-circle me-2"></i>
									SvelteKit Framework
								</div>
							</div>
							<div class="col-md-6">
								<div class="alert alert-info" role="alert">
									<i class="bi bi-info-circle me-2"></i>
									Bootstrap UI Components
								</div>
							</div>
						</div>
						
						<div class="mt-3">
							<a href="https://svelte.dev/docs/kit" class="btn btn-outline-secondary me-2" target="_blank">
								<i class="bi bi-book me-1"></i> SvelteKit Docs
							</a>
							<a href="https://getbootstrap.com/docs/5.3/" class="btn btn-outline-secondary" target="_blank">
								<i class="bi bi-bootstrap me-1"></i> Bootstrap Docs
							</a>
						</div>
						<h1>My Todos</h1>
						{#if error}
						  <p style="color: red;">Error: {error}</p>
						{/if}
						{#if isLoading}
						  <p>Loading...</p>
						{:else}
						  <button onclick={createTodo}>Add Todo</button>
						
						  {#each todos as todo (todo.id)}
							<div>
							  <span>{todo.content}</span>
							  <span>{todo.isDone ? '✓ Done' : '⏳ Pending'}</span>
							  <button onclick={() => updateTodo(todo.id, todo.isDone)}>
								Toggle
							  </button>
							  <button onclick={() => deleteTodo(todo.id)}>Delete</button>
							</div>
						  {/each}
						{/if}
					</div>
				</div>
			</div>
		</div>
	</div>
</div> 