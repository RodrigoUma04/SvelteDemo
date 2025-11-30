<script>
  import { Play, Code, Zap, Package, Server, FileCode } from 'lucide-svelte';
  
  let activeTab = 'comparison';
  let counter = 0;
  let name = '';
  
  // Reactive declarations - these update automatically when dependencies change
  $: doubled = counter * 2;
  $: squared = counter * counter;
  $: nameLength = name.length;
  
  const tabs = [
    { id: 'comparison', label: 'Quick Comparison', icon: Code },
    { id: 'reactivity', label: 'Svelte Reactivity', icon: Zap },
    { id: 'sveltekit', label: 'SvelteKit Features', icon: Server },
    { id: 'code', label: 'Code Examples', icon: FileCode }
  ];
  
  const features = [
    {
      title: "File-Based Routing",
      icon: "📁",
      description: "Create routes just by adding files",
      example: "src/routes/about/+page.svelte → /about"
    },
    {
      title: "Server-Side Rendering (SSR)",
      icon: "⚡",
      description: "Pages render on the server for fast load times and SEO",
      example: "Perfect for marketing sites, blogs, e-commerce"
    },
    {
      title: "API Routes",
      icon: "🔌",
      description: "Build backend endpoints in the same project",
      example: "src/routes/api/data/+server.js → /api/data"
    },
    {
      title: "Form Actions",
      icon: "📝",
      description: "Handle form submissions without JavaScript",
      example: "Progressive enhancement out of the box"
    },
    {
      title: "Code Splitting",
      icon: "✂️",
      description: "Automatically splits code per route",
      example: "Only load what you need, when you need it"
    },
    {
      title: "Adapters",
      icon: "🚀",
      description: "Deploy anywhere with adapters",
      example: "Vercel, Netlify, Cloudflare, Node, static"
    }
  ];
</script>

<div class="min-h-screen bg-gradient-to-br from-orange-50 to-red-50 p-8">
  <div class="max-w-6xl mx-auto">
    <!-- Header -->
    <div class="text-center mb-8">
      <h1 class="text-5xl font-bold text-orange-600 mb-2">
        Svelte & SvelteKit
      </h1>
      <p class="text-xl text-gray-600">
        The compile-time framework that changes everything
      </p>
    </div>

    <!-- Tab Navigation -->
    <div class="flex gap-2 mb-6 overflow-x-auto">
      {#each tabs as tab}
        <button
          on:click={() => activeTab = tab.id}
          class="flex items-center gap-2 px-4 py-3 rounded-lg font-medium transition-all whitespace-nowrap {activeTab === tab.id
            ? 'bg-orange-600 text-white shadow-lg'
            : 'bg-white text-gray-700 hover:bg-orange-100'}"
        >
          <svelte:component this={tab.icon} size={18} />
          {tab.label}
        </button>
      {/each}
    </div>

    <!-- Content Area -->
    <div class="bg-white rounded-xl shadow-2xl p-8">
      {#if activeTab === 'comparison'}
        <div>
          <h2 class="text-3xl font-bold text-gray-800 mb-6">
            Svelte vs SvelteKit: What's the Difference?
          </h2>
          
          <div class="grid md:grid-cols-2 gap-6 mb-8">
            <!-- Svelte Card -->
            <div class="border-2 border-orange-300 rounded-lg p-6 bg-orange-50">
              <div class="flex items-center gap-3 mb-4">
                <Package class="text-orange-600" size={32} />
                <h3 class="text-2xl font-bold text-orange-600">Svelte</h3>
              </div>
              <p class="text-gray-700 mb-4">
                <strong>Component Framework</strong> - Like React or Vue
              </p>
              <ul class="space-y-2 text-gray-700">
                <li>✅ Build UI components</li>
                <li>✅ Just 1.6kB gzipped</li>
                <li>✅ No virtual DOM</li>
                <li>✅ Compiles to vanilla JS</li>
                <li>✅ Built-in reactivity</li>
                <li>❌ No routing (needs libraries)</li>
                <li>❌ No SSR out of the box</li>
                <li>❌ Client-side only</li>
              </ul>
              <div class="mt-4 p-3 bg-white rounded border border-orange-200">
                <strong>Best for:</strong> Single-page apps, widgets, client-side projects
              </div>
            </div>

            <!-- SvelteKit Card -->
            <div class="border-2 border-red-300 rounded-lg p-6 bg-red-50">
              <div class="flex items-center gap-3 mb-4">
                <Server class="text-red-600" size={32} />
                <h3 class="text-2xl font-bold text-red-600">SvelteKit</h3>
              </div>
              <p class="text-gray-700 mb-4">
                <strong>Full-Stack Framework</strong> - Like Next.js or Nuxt
              </p>
              <ul class="space-y-2 text-gray-700">
                <li>✅ Everything Svelte can do</li>
                <li>✅ File-based routing</li>
                <li>✅ Server-side rendering (SSR)</li>
                <li>✅ API routes/endpoints</li>
                <li>✅ Form actions</li>
                <li>✅ Code splitting</li>
                <li>✅ Static site generation</li>
                <li>✅ Full-stack capabilities</li>
              </ul>
              <div class="mt-4 p-3 bg-white rounded border border-red-200">
                <strong>Best for:</strong> Multi-page apps, SEO-critical sites, full-stack projects
              </div>
            </div>
          </div>

          <div class="bg-gradient-to-r from-orange-100 to-red-100 p-6 rounded-lg">
            <h4 class="text-xl font-bold mb-3 text-gray-800">
              🎯 Quick Decision Guide
            </h4>
            <p class="text-gray-700 text-lg">
              <strong>Use Svelte:</strong> Building a front-end only app that calls external APIs<br/>
              <strong>Use SvelteKit:</strong> Need a server, SEO, routing, or building anything production-ready
            </p>
          </div>
        </div>
      {:else if activeTab === 'reactivity'}
        <div>
          <h2 class="text-3xl font-bold text-gray-800 mb-6">
            Svelte's Magic: True Reactivity
          </h2>
          
          <div class="mb-8">
            <h3 class="text-xl font-bold mb-4 text-orange-600">
              What Makes Svelte Different?
            </h3>
            <div class="bg-yellow-50 border-l-4 border-yellow-400 p-4 mb-6">
              <p class="text-gray-700">
                <strong>No Virtual DOM!</strong> React and Vue use a virtual DOM to track changes. 
                Svelte compiles your code at build time and knows exactly what changes when. 
                This means faster performance and smaller bundle sizes.
              </p>
            </div>
          </div>

          <!-- Interactive Demo -->
          <div class="border-2 border-orange-300 rounded-lg p-6 mb-6">
            <h3 class="text-xl font-bold mb-4 text-gray-800">
              Interactive Demo: Svelte-Style Reactivity
            </h3>
            
            <div class="space-y-6">
              <!-- Counter Example -->
              <div>
                <h4 class="font-bold mb-2 text-gray-700">1. Counter (Reactive Assignment)</h4>
                <div class="flex items-center gap-4">
                  <button
                    on:click={() => counter += 1}
                    class="bg-orange-600 text-white px-6 py-3 rounded-lg font-bold hover:bg-orange-700 transition"
                  >
                    Count: {counter}
                  </button>
                  <div class="text-gray-700">
                    <div>Double: <strong>{doubled}</strong></div>
                    <div>Square: <strong>{squared}</strong></div>
                  </div>
                </div>
                <p class="mt-2 text-sm text-gray-600">
                  In Svelte: Just write <code class="bg-gray-100 px-1">count += 1</code> and everything updates automatically!
                </p>
              </div>

              <!-- Name Example -->
              <div>
                <h4 class="font-bold mb-2 text-gray-700">2. Text Input (Two-way Binding)</h4>
                <input
                  type="text"
                  bind:value={name}
                  placeholder="Type your name..."
                  class="border-2 border-gray-300 rounded-lg px-4 py-2 w-full mb-2"
                />
                {#if name}
                  <div class="bg-orange-100 p-4 rounded-lg">
                    <p class="text-lg">Hello, <strong>{name}</strong>! 👋</p>
                    <p class="text-sm text-gray-600">
                      Your name has {nameLength} characters
                    </p>
                  </div>
                {/if}
                <p class="mt-2 text-sm text-gray-600">
                  In Svelte: Use <code class="bg-gray-100 px-1">bind:value</code> for automatic two-way binding
                </p>
              </div>
            </div>
          </div>

          <!-- Code Comparison -->
          <div class="grid md:grid-cols-2 gap-4">
            <div>
              <h4 class="font-bold mb-2 text-gray-700">React (verbose)</h4>
              <pre class="bg-gray-900 text-gray-100 p-4 rounded-lg overflow-x-auto text-sm">{`const [count, setCount] = useState(0)

<button 
  onClick={() => setCount(count + 1)}
>
  {count}
</button>`}</pre>
            </div>
            <div>
              <h4 class="font-bold mb-2 text-orange-600">Svelte (concise)</h4>
              <pre class="bg-orange-900 text-orange-100 p-4 rounded-lg overflow-x-auto text-sm">{`<script>
  let count = 0
</script>

<button on:click={() => count += 1}>
  {count}
</button>`}</pre>
            </div>
          </div>
        </div>
      {:else if activeTab === 'sveltekit'}
        <div>
          <h2 class="text-3xl font-bold text-gray-800 mb-6">
            SvelteKit: Full-Stack Superpowers
          </h2>

          <div class="space-y-6">
            <!-- Feature Cards -->
            {#each features as feature}
              <div class="border-2 border-red-200 rounded-lg p-6 bg-red-50 hover:shadow-lg transition">
                <div class="flex items-start gap-4">
                  <div class="text-4xl">{feature.icon}</div>
                  <div class="flex-1">
                    <h3 class="text-xl font-bold text-red-600 mb-2">
                      {feature.title}
                    </h3>
                    <p class="text-gray-700 mb-2">{feature.description}</p>
                    <code class="text-sm bg-white px-3 py-1 rounded border border-red-200 inline-block">
                      {feature.example}
                    </code>
                  </div>
                </div>
              </div>
            {/each}
          </div>

          <div class="mt-8 bg-gradient-to-r from-orange-100 to-red-100 p-6 rounded-lg">
            <h4 class="text-xl font-bold mb-3">🎯 Real-World Users</h4>
            <p class="text-gray-700">
              <strong>IKEA</strong> rebuilt their global site with SvelteKit<br/>
              <strong>The New York Times</strong> uses Svelte for interactive graphics<br/>
              <strong>Spotify</strong> built their "Wrapped" feature with Svelte
            </p>
          </div>
        </div>
      {:else if activeTab === 'code'}
        <div>
          <h2 class="text-3xl font-bold text-gray-800 mb-6">
            Code Examples: See the Difference
          </h2>

          <div class="space-y-8">
            <!-- Example 1 -->
            <div>
              <h3 class="text-xl font-bold mb-4 text-orange-600">
                1. Basic Component Structure
              </h3>
              <div class="bg-gray-900 text-gray-100 p-6 rounded-lg overflow-x-auto">
                <pre class="text-sm">{`<!-- App.svelte -->
<script>
  let count = 0;
  let name = 'world';
  
  // Reactive declaration - runs when count changes
  $: doubled = count * 2;
  
  function increment() {
    count += 1;  // That's it! No setState needed
  }
</script>

<style>
  /* Scoped styles - only apply to this component */
  h1 { color: orange; }
  button { 
    padding: 10px 20px;
    background: #ff3e00;
  }
</style>

<h1>Hello {name}!</h1>
<p>Count: {count}, Doubled: {doubled}</p>
<button on:click={increment}>
  Increment
</button>

<!-- Two-way binding -->
<input bind:value={name} />`}</pre>
              </div>
            </div>

            <!-- Example 2 -->
            <div>
              <h3 class="text-xl font-bold mb-4 text-orange-600">
                2. Conditional Rendering & Loops
              </h3>
              <div class="bg-gray-900 text-gray-100 p-6 rounded-lg overflow-x-auto">
                <pre class="text-sm">{`<script>
  let todos = [
    { id: 1, text: 'Learn Svelte', done: false },
    { id: 2, text: 'Build app', done: false }
  ];
  
  let showCompleted = true;
</script>

<!-- Conditional rendering -->
{#if showCompleted}
  <h2>All Todos</h2>
{:else}
  <h2>Active Todos</h2>
{/if}

<!-- Loop with keyed each block -->
{#each todos as todo (todo.id)}
  <div>
    <input type="checkbox" bind:checked={todo.done} />
    <span class:done={todo.done}>{todo.text}</span>
  </div>
{/each}`}</pre>
              </div>
            </div>

            <!-- Example 3 -->
            <div>
              <h3 class="text-xl font-bold mb-4 text-red-600">
                3. SvelteKit: Load Data on Server
              </h3>
              <div class="bg-gray-900 text-gray-100 p-6 rounded-lg overflow-x-auto">
                <pre class="text-sm">{`// src/routes/blog/+page.server.js
export async function load() {
  const posts = await fetch('https://api.example.com/posts')
    .then(r => r.json());
  
  return { posts };
}

<!-- src/routes/blog/+page.svelte -->
<script>
  export let data;  // Data from load function
</script>

<h1>Blog Posts</h1>
{#each data.posts as post}
  <article>
    <h2>{post.title}</h2>
    <p>{post.excerpt}</p>
  </article>
{/each}`}</pre>
              </div>
              <p class="mt-3 text-gray-600">
                ⚡ This runs on the server and sends HTML to the client - great for SEO!
              </p>
            </div>

            <!-- Example 4 -->
            <div>
              <h3 class="text-xl font-bold mb-4 text-red-600">
                4. SvelteKit: API Route
              </h3>
              <div class="bg-gray-900 text-gray-100 p-6 rounded-lg overflow-x-auto">
                <pre class="text-sm">{`// src/routes/api/random/+server.js
export function GET({ url }) {
  const min = Number(url.searchParams.get('min')) || 0;
  const max = Number(url.searchParams.get('max')) || 100;
  
  const random = Math.floor(
    Math.random() * (max - min + 1) + min
  );
  
  return new Response(
    JSON.stringify({ value: random }),
    { headers: { 'Content-Type': 'application/json' } }
  );
}

// Access at: /api/random?min=0&max=100`}</pre>
              </div>
            </div>
          </div>

          <div class="mt-8 bg-blue-50 border-l-4 border-blue-500 p-6">
            <h4 class="font-bold text-lg mb-2">💡 Key Takeaways</h4>
            <ul class="space-y-2 text-gray-700">
              <li>✅ <strong>Less boilerplate:</strong> No useState, no useEffect, just variables</li>
              <li>✅ <strong>Reactive by default:</strong> Use $: for reactive declarations</li>
              <li>✅ <strong>Built-in directives:</strong> bind:, on:, class:, etc.</li>
              <li>✅ <strong>Scoped styles:</strong> CSS only affects the current component</li>
              <li>✅ <strong>Full-stack in SvelteKit:</strong> Load data on server, build APIs</li>
            </ul>
          </div>
        </div>
      {/if}
    </div>

    <!-- Footer -->
    <div class="mt-8 text-center text-gray-600">
      <p class="mb-2">
        <strong>Want to learn more?</strong>
      </p>
      <div class="flex justify-center gap-4 flex-wrap">
        <span class="bg-white px-4 py-2 rounded-lg shadow">
          📚 <a href="https://svelte.dev/tutorial" class="text-orange-600 hover:underline" target="_blank" rel="noopener noreferrer">Svelte Tutorial</a>
        </span>
        <span class="bg-white px-4 py-2 rounded-lg shadow">
          🚀 <a href="https://learn.svelte.dev" class="text-red-600 hover:underline" target="_blank" rel="noopener noreferrer">SvelteKit Tutorial</a>
        </span>
      </div>
    </div>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
  }
</style>