<script>
    import { deleteDoc, doc, getDoc } from 'firebase/firestore';
    import { page } from '$app/stores';
    import { onMount } from 'svelte';
    import { db } from '../../../firebase';
   
    let task = {};
   
    const id = $page.params.id;
   
    onMount(async () => {
     const ref = doc(db, 'tasks', id);
     const snapshot = await getDoc(ref);
     task = { id: snapshot.id, ...snapshot.data() };
    });
   
    const handleDelete = async () => {
     const ref = doc(db, 'tasks', id);
     deleteDoc(ref)
      .then(() => {
       alert('Item deleted successfully!');
       window.location.href = '/';
      })
      .catch((error) => {
       console.log(error);
      });
    };
   </script>
   
   <div class="container mx-auto mt-8 max-w-[560px]">
    <div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
     <h1 class="text-3xl font-semibold">Delete Task</h1>
    </div>
    <div class="my-12">
     Are you sure to delete <strong>{task?.name}</strong>?
    </div>
    <div class="flex w-full gap-2">
     <a
      href="/"
      class="text-center bg-gray-300 hover:bg-opacity-80 text-black rounded-lg px-4 py-2 duration-200 w-full"
     >
      Cancel
     </a>
     <button
      class="bg-red-500 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200 w-full"
      type="button"
      on:click={handleDelete}
     >
      Delete
     </button>
    </div>
   </div>