<script>
    import { addDoc, collection } from 'firebase/firestore';
    import { db } from '../../firebase';
    let name = '';
    let description = '';
   
    const handleCreate = async () => {
     const col = collection(db, 'tasks');
     await addDoc(col, {
      name,
      description
     });
     name = '';
     description = '';
     alert('Item added successfully!');
     window.location.href = '/';
    };
   </script>
   
   <div class="container mx-auto mt-8 max-w-[560px]">
    <div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
     <h1 class="text-3xl font-semibold">Create Task</h1>
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
   
    <button
     on:click={handleCreate}
     class="bg-green-600 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200 w-full"
     >Create Task</button
    >
   </div>