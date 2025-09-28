<script>
  import { onMount } from "svelte";
  import { Toaster, toast } from "svelte-sonner";

  let persons = [];
  let name = "";
  let email = "";
  let editId = null;

  const API_URL = "http://localhost:5000/api/persons";

  // fetch all persons from backend
  async function loadPersons() {
    try {
      const res = await fetch(API_URL);
      persons = await res.json();
    } catch (err) {
      toast.error("Failed to load persons");
      console.error(err);
    }
  }

  onMount(() => {
    loadPersons();
  });

  async function addPerson() {
    if (!name || !email) {
      toast.error("Name and email required");
      return;
    }

    try {
      if (editId) {
        const res = await fetch(`${API_URL}/${editId}`, {
          method: "PUT",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ name, email }),
        });
        const updated = await res.json();
        persons = persons.map((p) => (p._id === editId ? updated : p));
        toast.success("Person updated");
        editId = null;
      } else {
        const res = await fetch(API_URL, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ name, email }),
        });
        const newPerson = await res.json();
        persons = [...persons, newPerson];
        toast.success("Person added");
      }
      name = "";
      email = "";
    } catch (err) {
      toast.error("Failed to save person");
      console.error(err);
    }
  }

  function editPerson(p) {
    name = p.name;
    email = p.email;
    editId = p._id;
  }

  async function deletePerson(id) {
    try {
      await fetch(`${API_URL}/${id}`, { method: "DELETE" });
      persons = persons.filter((p) => p._id !== id);
      toast.success("Person deleted");
    } catch (err) {
      toast.error("Failed to delete person");
      console.error(err);
    }
  }
</script>

<main class="min-h-screen bg-gray-100 p-6">
  <h1 class="text-2xl font-bold mb-4">Person Manager</h1>

  <!-- Form -->
  <form class="space-y-3" on:submit|preventDefault={addPerson}>
    <input
      type="text"
      placeholder="Name"
      bind:value={name}
      class="w-full p-2 border rounded"
    />
    <input
      type="email"
      placeholder="Email"
      bind:value={email}
      class="w-full p-2 border rounded"
    />
    <button
      type="submit"
      class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700"
    >
      {editId ? "Update Person" : "Add Person"}
    </button>
  </form>

  <!-- List -->
  <ul class="mt-6 space-y-2">
    {#each persons as p}
      <li class="flex justify-between items-center p-3 bg-white shadow rounded">
        <div>
          <p class="font-semibold">{p.name}</p>
          <p class="text-sm text-gray-600">{p.email}</p>
        </div>
        <div class="space-x-2">
          <button
            class="px-2 py-1 text-sm bg-yellow-500 text-white rounded hover:bg-yellow-600"
            on:click={() => editPerson(p)}
          >
            Edit
          </button>
          <button
            class="px-2 py-1 text-sm bg-red-500 text-white rounded hover:bg-red-600"
            on:click={() => deletePerson(p._id)}
          >
            Delete
          </button>
        </div>
      </li>
    {/each}
  </ul>

  <Toaster richColors position="top-right" />
</main>
