<script lang="ts">
	import { collection, getDocs } from 'firebase/firestore';
	import { db } from '../firebase';
	import { onMount } from 'svelte';
   
	let items: any[] = [];
   
	onMount(async () => {
	 const ref = collection(db, 'tasks');
	 const snapshot = await getDocs(ref);
	 items = snapshot.docs.map((doc) => ({ id: doc.id, ...doc.data() }));
	});
   </script>
   
   <div class="container mx-auto mt-8 max-w-[560px]">
	<div class="flex justify-between items-center pb-4 border-b border-dashed border-gray-900 mb-4">
	 <h1 class="text-3xl font-semibold">Tasks</h1>
	 <a
	  href="/create"
	  class="bg-green-600 hover:bg-opacity-80 text-white rounded-lg px-4 py-2 duration-200"
	  >Create Task</a
	 >
	</div>
	<ul>
	 {#each items as item}
	  <li class="py-2 flex justify-between w-full">
	   <span>
		<strong>{item.name}</strong> - {item.description}
	   </span>
	   <span class="flex gap-2">
		<a href={`/${item.id}/edit`} class="text-blue-700 underline hover:no-underline">Edit</a>
		<a href={`/${item.id}/delete`} class="text-red-500 underline hover:no-underline">Delete</a
		>
	   </span>
	  </li>
	 {/each}
	</ul>
   </div>