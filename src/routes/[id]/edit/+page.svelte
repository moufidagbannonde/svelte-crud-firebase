<script>
    import { doc, getDoc, setDoc } from 'firebase/firestore';
    import { page } from '$app/stores';
    import { onMount } from 'svelte';
    import { db } from '../../../firebase';
   
    let name = '';
    let description = '';
   
    const id = $page.params.id;
   
    onMount(async () => {
     const ref = doc(db, 'tasks', id);
     const snapshot = await getDoc(ref);
     name = snapshot.data()?.name;
     description = snapshot.data()?.description;
    });
   
    const handleUpdate = async () => {
     const ref = doc(db, 'tasks', id);
     setDoc(ref, {
      name,
      description
     })
      .then(() => {
       alert('Item updated successfully!');
       window.location.href = '/';
      })
      .catch((error) => {
       console.log(error);
      });
    };
   </script>
   
   <div class="container mx-auto mt-8 max-w-[560px]">
    <div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
     <h1 class="text-3xl font-semibold">Edit Task</h1>
    </div>
    <div class="mb-4">
     <p>Title</p>
     <input
      bind:value={name}
      placeholder="Name"
      class="mt-1 px-4 py-2 border border-gray-300 rounded-md block w-full"
     />
    </div>
    <div class="mb-4">
     <p>Description</p>
     <input
      bind:value={description}
      placeholder="Description"
      class="mt-1 px-4 py-2 border border-gray-300 rounded-md block w-full"
     />
    </div>
    <div class="flex w-full gap-2">
     <a
      href="/"
      class="text-center bg-gray-300 hover:bg-opacity-80 text-black rounded-lg px-4 py-2 duration-200 w-full"
     >
      Cancel
     </a>
     <button
      on:click={handleUpdate}
      class="bg-green-600 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200 w-full"
      >Edit Task</button
     >
    </div>
   </div>