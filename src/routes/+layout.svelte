<script>
	import { onMount } from "svelte";
	import NavBar from "$lib/components/nav.svelte"
	import About from './sections/about.svelte'
	import Stack from './sections/stack.svelte'
	import Services from './sections/services.svelte'
	import Projects from './sections/projects.svelte'
	import Testimonials from './sections/testimonials.svelte'
	import Contact from './sections/contact.svelte'
	import '../app.css';



	let { children } = $props();

	

</script>



<div class="min-h-screen w-full relative bg-[#FFFFFF] overflow-hidden">

	<NavBar />

	{@render children()}



	<div id="about">
		<About/>
	</div>
	<div  >
		<Testimonials />
	</div>
	<div id="stack">
		<Stack/>
	</div>
	<div id="services" >
		<Services />
	</div>
	<div id="projects" >
		<Projects/>
	</div>
	<div id="contact" class="h-screen" >
		<Contact/>
	</div>

	
</div>