<script>
	import { onMount } from "svelte";
	import { gsap } from "gsap";

    let { data } = $props();
    let activeSection = $state('home');
	let sections = [];
	let isMenuOpen = $state(false);
	let isMobile = $state(false);

	function toggleMenu() {
		isMenuOpen = !isMenuOpen;
		
		if (isMenuOpen) {
			gsap.to(".mobile-menu", {
				x: 0,
				opacity: 1,
				duration: 0.3,
				ease: "power2.out"
			});
		} else {
			gsap.to(".mobile-menu", {
				x: "100%",
				opacity: 0,
				duration: 0.3,
				ease: "power2.in"
			});
		}
	}

	function handleScroll() {
		const scrollPosition = window.scrollY + 100;
		for (const section of sections) {
			const sectionTop = section.offsetTop;
			const sectionHeight = section.offsetHeight;

			if (scrollPosition >= sectionTop && scrollPosition < sectionTop+sectionHeight) {
				activeSection = section.id;
				break;
			}
		}
	}

	function scrollToElement(id) {
		const section = document.getElementById(id);
		if (section) {
			window.scrollTo({
				top: section.offsetTop,
				behavior: 'smooth'
			});
		}
		activeSection = id;
		
		// Close menu on mobile after clicking a link
		if (isMobile) {
			toggleMenu();
		}
	}

	function checkScreenSize() {
		isMobile = window.innerWidth < 768;
		
		// Make sure mobile menu is hidden when switching to desktop
		if (!isMobile && isMenuOpen) {
			isMenuOpen = false;
			gsap.set(".mobile-menu", { x: "100%", opacity: 0 });
		}
	}

	onMount(() => {
		sections = [
			document.getElementById('home'),
			document.getElementById('about'),
			document.getElementById('stack'),
			document.getElementById('services'),
			document.getElementById('projects'),
			document.getElementById('contact')
		].filter(Boolean);
		
		document.addEventListener('scroll', handleScroll);
		
		// Check screen size on mount and add resize listener
		checkScreenSize();
		window.addEventListener('resize', checkScreenSize);

		return () => {
			window.removeEventListener('scroll', handleScroll);
			window.removeEventListener('resize', checkScreenSize);
		}
	});
</script>

<!-- Desktop Navigation -->
<nav class="z-50 w-full md:w-2/3 lg:w-1/2 h-5px bg-[#EFF0FF] fixed left-1/2 -translate-x-1/2 mt-4 shadow-2xl rounded-full hidden md:block">
    <ul class="flex flex-row justify-between w-full p-1">
        <li class="p-4 font-[500] text-[14px] transform transition-transform duration-300 {activeSection === 'home' ? 'bg-[#F94706] rounded-full text-white' : 'hover:-translate-y-1'}" on:click={() => scrollToElement('home')}>Home</li>
        <li class="p-4 font-[500] text-[14px] transform transition-transform duration-300 {activeSection === 'about' ? 'bg-[#F94706] rounded-full text-white' : 'hover:-translate-y-1'}" on:click={() => scrollToElement('about')}>About</li>
        <li class="p-4 font-[500] text-[14px] transform transition-transform duration-300 {activeSection === 'stack' ? 'bg-[#F94706] rounded-full text-white' : 'hover:-translate-y-1'}" on:click={() => scrollToElement('stack')}>Stack</li>
        <li class="p-4 font-[500] text-[14px] transform transition-transform duration-300 {activeSection === 'services' ? 'bg-[#F94706] rounded-full text-white' : 'hover:-translate-y-1'}" on:click={() => scrollToElement('services')}>Services</li>
        <li class="p-4 font-[500] text-[14px] transform transition-transform duration-300 {activeSection === 'projects' ? 'bg-[#F94706] rounded-full text-white' : 'hover:-translate-y-1'}" on:click={() => scrollToElement('projects')}>Projects</li>
        <li class="p-4 font-[500] text-[14px] transform transition-transform duration-300 {activeSection === 'contact' ? 'bg-[#F94706] rounded-full text-white' : 'hover:-translate-y-1'}" on:click={() => scrollToElement('contact')}>Contact</li>
    </ul>
</nav>

<!-- Mobile Hamburger Button -->
<div class="fixed top-4 right-4 z-50 md:hidden">
    <button 
        class="p-2 bg-[#EFF0FF] rounded-lg shadow-md focus:outline-none"
        on:click={toggleMenu}
        aria-label="Toggle menu"
    >
        {#if isMenuOpen}
            <!-- X icon for close -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke={activeSection ? '#F94706' : 'currentColor'}>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
        {:else}
            <!-- Hamburger icon -->
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke={activeSection ? '#F94706' : 'currentColor'}>
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
        {/if}
    </button>
</div>

<!-- Mobile Menu - Add initial transform and opacity styles directly -->
<div class="mobile-menu fixed top-0 right-0 h-full w-64 bg-[#EFF0FF] shadow-2xl z-40 flex flex-col md:hidden" style="transform: translateX(100%); opacity: 0;">
    <div class="p-4 mt-16">
        <ul class="flex flex-col space-y-4">
            <li class="p-3 font-[500] text-center transition-colors duration-300 {activeSection === 'home' ? 'bg-[#F94706] rounded-full text-white' : 'hover:bg-gray-200 rounded-full'}" on:click={() => scrollToElement('home')}>Home</li>
            <li class="p-3 font-[500] text-center transition-colors duration-300 {activeSection === 'about' ? 'bg-[#F94706] rounded-full text-white' : 'hover:bg-gray-200 rounded-full'}" on:click={() => scrollToElement('about')}>About</li>
            <li class="p-3 font-[500] text-center transition-colors duration-300 {activeSection === 'stack' ? 'bg-[#F94706] rounded-full text-white' : 'hover:bg-gray-200 rounded-full'}" on:click={() => scrollToElement('stack')}>Stack</li>
            <li class="p-3 font-[500] text-center transition-colors duration-300 {activeSection === 'services' ? 'bg-[#F94706] rounded-full text-white' : 'hover:bg-gray-200 rounded-full'}" on:click={() => scrollToElement('services')}>Services</li>
            <li class="p-3 font-[500] text-center transition-colors duration-300 {activeSection === 'projects' ? 'bg-[#F94706] rounded-full text-white' : 'hover:bg-gray-200 rounded-full'}" on:click={() => scrollToElement('projects')}>Projects</li>
            <li class="p-3 font-[500] text-center transition-colors duration-300 {activeSection === 'contact' ? 'bg-[#F94706] rounded-full text-white' : 'hover:bg-gray-200 rounded-full'}" on:click={() => scrollToElement('contact')}>Contact</li>
        </ul>
    </div>
</div>

<!-- Overlay for mobile menu -->
{#if isMenuOpen}
<div 
    class="fixed inset-0 bg-black bg-opacity-50 z-30 md:hidden" 
    on:click={toggleMenu}
></div>
{/if}