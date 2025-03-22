<script>
    import { onMount } from "svelte";
    import { fly } from "svelte/transition";


    const rotatingText = [
        'Branding',
        'UI/UX Design',
        'Mobile App',
        'Web Dev',
        'AI/Gen AI',
        'Computer Vision',
    ]
    let currentIndex = $state(0);


    $effect(() => {
		const interval = setInterval(() => {
			currentIndex += 1;
			currentIndex %= rotatingText.length;
            console.log(currentIndex);

        }, 1300);

		return () => {
			clearInterval(interval);
		};
	});

    onMount(() => {
        setTimeout(() => {
            const images = document.querySelectorAll('.shape-img');
            images.forEach(img => {
            img.classList.remove('scale-75');
            img.classList.add('scale-100');
            });
            
            setTimeout(() => {
            images.forEach(img => {
                img.classList.add('animate-floating');
            });
            }, 1000); 
        }, 200);
    });

    

</script>



<div id="home" class="h-screen w-full relative
flex flex-col justify-center items-center bg-[#FFFFFF] overflow-hidden">
    
    <div class="h-screen w-full absolute top-0 left-0 bg-transparent lg:z-10">
        <div class="relative h-screen w-full">
            <img class="shape-img absolute h-[20vh] top-20 left-1  lg:top-6 lg:left-72 lg:h-[280px] transform  scale-75 transition-all duration-1000 ease-out" src="shape_pyramid.avif" alt="">
            <img class="shape-img absolute z-30 top-1/3 -left-6 lg:top-52 lg:left-48 h-[20vh] lg:h-[280px] scale-75 transition-all duration-1000 ease-out" src="shape_sphere.avif" alt="">
            <img class="shape-img absolute bottom-4 left-0 lg:bottom-0 lg:left-72 h-[20vh] lg:h-[280px] scale-75 transition-all duration-1000 ease-out" src="shape_star.avif" alt="">
            
            <img class="shape-img absolute h-[20vh] top-20 right-1 lg:top-6 lg:right-72  lg:h-[280px] scale-75 transition-all duration-1000 ease-out" src="shape_cuba.avif" alt="">
            <img class="shape-img absolute z-30 lg:z-0 top-[50%] -right-5 lg:top-56 lg:right-48 h-[26vh] lg:h-[280px] scale-75 transition-all duration-1000 ease-out" src="shape_cube.avif" alt="">
            <img class="shape-img absolute bottom-12 right-0 lg:bottom-0 lg:right-72 h-[20vh] lg:h-[280px] transform  scale-75 transition-all duration-1000 ease-out" src="shape_cylinder.avif" alt="">
        </div>
    </div>

    <div class="z-0 h-screen w-full absolute top-0 left-0  flex justify-center items-center  pointer-events-none">
        <div class="animate-marquee whitespace-nowrap">
            <h1 
            class="text-[240px] tracking-wide text-nowrap font-black font-public text-black overflow-hidden "
            >
            Shahzaib Khakwani <span> </span> 
            </h1>
        </div>
        <div class="absolute  py-12 animate-marquee2 whitespace-nowrap">
            <h1 
            class="ml-8 tracking-wide text-[240px] text-nowrap font-black font-public text-black overflow-hidden "
            >
                Shahzaib Khakwani
            </h1>
        </div>
    </div>

    <div class="z-20">
        <h1 class="font-public text-4xl font-medium leading-[2]">Hi I am <span class='font-serif font-[48px] font-bold italic'>Shahzaib</span>!</h1>
        {#key currentIndex}
        <h3
        in:fly={{y:'100%'}}
        class="
        overflow-hidden
        text-[#666666] text-center text-[24px] font-public"
        >{rotatingText[currentIndex]}</h3>
        {/key}
    </div>

    <div class="z-20 my-8 perspective-[1000px] group">
    

            <div class="relative [transform-style:preserve-3d] transition-transform duration-500  group-hover:[transform:rotateY(180deg)] h-72 w-72">
                <!-- Front of card -->
                <div class="absolute bg-[#6670FF] [backface-visibility:hidden] rounded-[3vw] h-full w-full overflow-hidden transform ">
                    <div class="h-full w-full flex items-center justify-center text-white text-2xl">
                        <img src="person.avif" class="absolute top-[10px] object-contain">
                    </div>
                </div>
                
                <!-- Back of card -->
                <div class="absolute bg-white/10 backdrop-blur-lg border border-white/20 shadow-lg [backface-visibility:hidden] [transform:rotateY(180deg)] rounded-[3vw] h-full w-full overflow-hidden">
                    <div class="h-full w-full flex items-center justify-center  ">
                    <svg class="animate-bounce" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 256 256" focusable="false" color="var(--token-1dfb5f8e-6d59-4a6a-bbc6-917bc568117f, rgb(0, 0, 0))" style="user-select: none; width: 40%; height: 40%; display: inline-block; fill: var(--token-1dfb5f8e-6d59-4a6a-bbc6-917bc568117f, rgb(0, 0, 0)); color: var(--token-1dfb5f8e-6d59-4a6a-bbc6-917bc568117f, rgb(0, 0, 0)); flex-shrink: 0;"><g color="var(--token-1dfb5f8e-6d59-4a6a-bbc6-917bc568117f, rgb(0, 0, 0))" weight="thin"><path d="M202.83,146.83l-72,72a4,4,0,0,1-5.66,0l-72-72a4,4,0,0,1,5.66-5.66L124,206.34V40a4,4,0,0,1,8,0V206.34l65.17-65.17a4,4,0,0,1,5.66,5.66Z"></path></g></svg>
                        
                        <svg  viewBox="0 0 100 100"  style="width: 80%; height: 80%; position: absolute;  will-change: transform;   transform: rotate(360deg);">
                            <path id="curve-wnxkz4" d="M 0 50 L 0 50 A 1 1 0 0 1 100 50 L 100 50 L 100 50 A 1 1 0 0 1 0 50 L 0 50" stroke-width="none" fill="transparent"></path>
                            <g class="animate-spin origin-center">
                                <text>
                                    <textPath href="#curve-wnxkz4" startOffset="0" dominant-baseline="Hanging" style="font-family: &quot;Public Sans&quot;, &quot;Public Sans Placeholder&quot;, sans-serif; font-size: 12px; font-style: normal; font-weight: 400; letter-spacing: 0em; line-height: 1em; word-spacing: 7px; fill: var(--token-1dfb5f8e-6d59-4a6a-bbc6-917bc568117f, rgb(0, 0, 0));">
                                        ✦  SCROLL DOWN  ✦ AND KNOW ME BETTER
                                    </textPath>
                                </text>
                            </g>
                        </svg>
                    </div>
                </div> 
            </div>
    
    </div>

    <div class="overflow-hidden z-20">
        <button class="overflow-hidden bg-transparent border-[#EFF0FF] border-8 flex justify-center items-center text-black text-[24px] font-bold font-public rounded-full border transition-all duration-300 ease-in-out group">
            <span class="p-4">Let's Work Together</span>
            <div class="overflow-hidden w-0 transition-all duration-300 ease-in-out group-hover:w-16">
                <img src="arrow.svg" 
                    class="w-16 h-16 opacity-0 transform transition-all duration-300 ease-in-out group-hover:opacity-100 group-hover:-rotate-90" 
                    alt="Icon description">
            </div>
        </button>
    </div>
</div>

<style>
    .animate-spin {
        animation-duration: 20s !important; /* Adjust this value as needed - higher means slower */
            }
    .animate-bounce {
        animation-duration: 1.5s !important; /* Adjust this value as needed - higher means slower */
            }
</style>