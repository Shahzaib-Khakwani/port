<script>
    import Card from "$lib/components/card.svelte";
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";
    
    let cardOneRef;
    let cardTwoRef;
    let cardThirdRef;
    let buttonRef;
    let titleRef;
    let isMobile;

    // Responsive handler
    function checkMobile() {
        isMobile = window.innerWidth < 768;
        return isMobile;
    }

    gsap.registerPlugin(ScrollTrigger);
    onMount(() => {
        // Initial check
        checkMobile();
        
        // Add resize listener
        window.addEventListener('resize', checkMobile);
        
        // Configure animations with responsive settings
        const tl = gsap.timeline({
            scrollTrigger: {
                trigger: '#about1',
                pin: true,
                start: 'top top',
                end: isMobile ? '150%+=200px top' : '100%+=200px top',
                scrub: 1,
                markers: false,
            }
        });

        tl.from(cardOneRef, {
            opacity: 0,
            rotate: isMobile ? -2 : -5,
            y: isMobile ? 50 : 100,
        }).from(cardTwoRef, {
            opacity: 0,
            rotate: isMobile ? 2 : 5,
            y: isMobile ? 50 : 100,
        }, ">").to(titleRef, {
            y: isMobile ? 50 : 100,
            opacity: 0,
        }, "<").from(cardThirdRef, {
            opacity: 0,
            rotate: isMobile ? 2 : 5,
            y: isMobile ? 50 : 100,
        }, ">").from(buttonRef, {
            opacity: 0,
            y: isMobile ? -50 : -100,
        }, ">");
        
        // Cleanup listener
        return () => {
            window.removeEventListener('resize', checkMobile);
        };
    });
</script>

<div id="about1" class="relative min-h-screen w-full flex flex-col justify-center items-center bg-[#FFFFFF] px-4 py-8 md:px-0 md:py-0">
    
    <div class="h-screen w-full absolute top-0 left-0 bg-transparent z-10">
        <div class="relative h-screen w-full">
            <img class="shape-img absolute top-1/3 -left-32 lg:top-2/5 lg:left-48 lg:h-[600px] transform  scale-75 transition-all duration-1000 ease-out" src="about_pyramid.avif" alt="">
            <img class="shape-img absolute top-1/2 -right-36  lg:top-1/3 lg:right-48 lg:h-[600px] scale-75 transition-all duration-1000 ease-out" src="about_cube.avif" alt="">
        </div>
    </div>

    
    <h1 bind:this={titleRef} class="z-20 text-2xl md:text-[38px] font-public font-medium mb-4 text-center">
        About
    </h1>
    <div class="z-20 relative w-full md:h-[40%] flex flex-col items-center">
        <div class="absolute -top-1/3 left-1/2 transform -translate-x-1/2 w-full sm:w-11/12 md:w-4/5 max-w-2xl" bind:this={cardOneRef}>
            <Card text='Proficient Django developer with mid-level expertise
Full-stack developer with specialization in SvelteKit development as well as Django implementation
The developer completed the development of web applications which included e-commerce functionality along with chat capabilities and blogging features.'/>
        </div>
        <div class="absolute -top-1/3 left-1/2 transform -translate-x-1/2 w-full sm:w-11/12 md:w-4/5 max-w-2xl" bind:this={cardTwoRef}>
            <Card text='Skilled in front-end technologies: GSAP, Tailwind CSS, dynamic interfaces
Grads of Coursera gained certification in Django Development and Advanced CNNs with TensorFlow.
The development of durable and scalable web solutions is among my professional capabilities.
Strong focus on delivering high-quality, value-driven project outcomes.'/>
        </div>
        
        
    </div>
    <div bind:this={buttonRef} class="z-20 absolute left-1/2 bottom-[5%] lg:-bottom-[3%] mt-4  transform -translate-x-1/2">
        <div class="overflow-hidden">
            <button class="overflow-hidden bg-transparent border-[#EFF0FF] border-4 md:border-8 flex justify-center items-center text-black text-base md:text-[24px] font-bold font-public rounded-full border transition-all duration-300 ease-in-out group">
                <span class="p-2 md:p-4">Read MY CV</span>
                <div class="overflow-hidden w-0 transition-all duration-300 ease-in-out group-hover:w-10 md:group-hover:w-16">
                    <img src='doc.svg' 
                        class="w-10 h-10 md:w-16 md:h-16 opacity-0 transform transition-all duration-300 ease-in-out group-hover:opacity-100 group-hover:-rotate-360 rounded-full" 
                        alt="Icon description">
                </div>
            </button>
        </div>
    </div>
</div>