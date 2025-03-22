<script>
    import { onMount } from "svelte";
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

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
        window.addEventListener('resize', handleResize);
        
        setupScrollTriggers();
        
        // Cleanup listener
        return () => {
            window.removeEventListener('resize', handleResize);
        };
    });
    
    function handleResize() {
        const wasMobile = isMobile;
        const nowMobile = checkMobile();
        
        // Only refresh ScrollTrigger instances if mobile state changed
        if (wasMobile !== nowMobile) {
            // Kill all existing scroll triggers
            ScrollTrigger.getAll().forEach(trigger => trigger.kill());
            // Reinitialize scroll triggers with new settings
            setupScrollTriggers();
        }
    }
    
    function setupScrollTriggers() {
        const sections = document.querySelectorAll('.section');
        const currentHeading = document.getElementById('current-heading');
        const currentDesc = document.getElementById('current-heading-number');
        
        // Don't set up GSAP for mobile
        if (isMobile) {
            // Just set the initial heading
            if (sections.length > 0) {
                updateHeading(sections[0]);
            }
            return;
        }
        
        sections.forEach((section, index) => {
            if (index === sections.length - 1) {
                ScrollTrigger.create({
                    trigger: section,
                    start: 'top top',
                    end: '100 top',
                    pin: "#headingSection",
                    onEnter: () => updateHeading(section),
                    onEnterBack: () => updateHeading(section),
                    markers: false
                });
            } else {
                ScrollTrigger.create({
                    trigger: section,
                    start: 'top top',
                    end: 'bottom top',
                    pin: "#headingSection",
                    onEnter: () => updateHeading(section),
                    onEnterBack: () => updateHeading(section),
                    markers: false
                });                
            }
        });
    }
    
    function updateHeading(section) {
        const heading = section.getAttribute('data-heading');
        const desc = section.getAttribute('data-no');
        const currentHeading = document.getElementById('current-heading');
        const currentDesc = document.getElementById('current-heading-number');
        
        if (currentHeading && currentDesc) {
            currentHeading.textContent = heading;
            currentDesc.textContent = desc;
        }
    }
</script>

{#snippet textSection(title, no, imgSrc = "", caption, imgAlt = "")}
    <div class="section md:min-h-screen py-8 md:py-0 md:flex md:flex-col md:items-center md:justify-center md:p-8" data-no={no} data-heading={title}>
        <!-- Mobile/Tablet Layout (flex column) -->
        <div class="md:hidden flex flex-col items-center">
            <!-- Mobile heading and number -->
            <div class="mb-4">
                <p class="text-[#f2f2f2] text-6xl font-extrabold text-center">{no}</p>
                <h2 class="text-center p-2 text-xl font-public font-bold">{title}</h2>
            </div>
            
            <!-- Image section for mobile/tablet -->
            {#if imgSrc}
                <div class="w-full max-w-md mb-6 flex justify-center">
                    <img src={imgSrc} alt={imgAlt} class="w-1/2 object-contain animate-floating">
                </div>
            {/if}
            
            <!-- Caption for mobile/tablet -->
            <div class="max-w-2xl w-full">
                <p class="text-[#4d4d4d] text-base sm:text-lg mb-4">{caption}</p>
            </div>
        </div>
        
        <!-- Desktop Layout (hidden on mobile) -->
        <div class="hidden md:block md:w-full">
            <div class="flex flex-col items-center">

                
                <!-- Image section for desktop - centered above caption -->
                {#if imgSrc}
                    <div class="w-full max-w-2xl mb-8 flex justify-center">
                        <img src={imgSrc} alt={imgAlt} class="w-1/3 object-contain animate-floating">
                    </div>
                {/if}
                
                <!-- Caption for desktop -->
                <div class="max-w-2xl w-full">
                    <p class="text-[#4d4d4d] text-xl">{caption}</p>
                </div>
            </div>
        </div>
    </div>
{/snippet}

<div class="min-h-screen w-full flex flex-col justify-center items-center bg-[#FFFFFF]">
    <div class="w-full py-8 md:h-24 text-center">
        <h1 class="font-public text-2xl md:text-[38px] text-center font-medium">
            Services
        </h1>
    </div>
    
    <div class="relative flex flex-col md:flex-row w-full px-4 md:p-16">
        <!-- Fixed heading section (only visible on desktop) -->
        <div id="headingSection" class="hidden md:flex md:w-[30%] md:h-screen md:relative md:flex-col md:justify-center md:items-center">
            <p id="current-heading-number" class="absolute w-full text-center z-10 text-[200px] text-[#f2f2f2] font-extrabold">01</p>
            <h1 id="current-heading" class="z-20 w-full bg-white text-center p-4 mt-24 text-[1.75rem] font-public font-bold transition-all duration-500">Website Development</h1>
        </div>
        
        <!-- Content section -->
        <div class="w-full md:w-[60%] md:p-4">
            {@render textSection("Website Development", "01", 'services1.avif', "Landing pages are laser-focused on specific marketing goals. We design high-impact landing pages that grab attention, communicate your value proposition clearly, and seamlessly convert visitors into leads or paying customers. From crafting compelling headlines and captivating visuals to optimizing conversion elements like CTAs (calls to action) and lead capture forms, we ensure your landing page delivers a powerful first impression and drives results.")}
            {@render textSection("Landing Page Design", "02", 'services2.avif', "Transform your vision into a reality. This service encompasses crafting beautiful and user-friendly websites that not only captivate visitors but also guide them towards specific actions, whether it's making a purchase, signing up for a newsletter, or contacting you. Our process involves in-depth understanding of your target audience, user experience (UX) design to ensure intuitive navigation and clear calls to action, and front-end development utilizing the latest web technologies to create a visually stunning and functional website.")}
            {@render textSection("E-commerce Design", "03", 'services3.avif', "Your online store should be a seamless shopping experience. We create user-friendly and visually appealing e-commerce websites that not only showcase your products beautifully but also make it easy for customers to browse, find what they're looking for, and complete their purchases effortlessly. We incorporate clear product information, intuitive navigation, secure payment gateways, and a streamlined checkout process to maximize sales conversions.")}
            {@render textSection("Website Prototyping", "04", 'services4.avif', "Don't wait until development begins to see your website come to life. We utilize advanced prototyping tools like Framer to build interactive prototypes that simulate the final user experience. These prototypes allow you to test user flow, visualize interactions, and gather valuable feedback before any code is written. This iterative process ensures your website is on the right track from the very beginning.")}
            {@render textSection("Responsive Design", "05", 'services5.avif', "Your website needs to look great and function flawlessly across all devices, from desktop computers to tablets and smartphones. Our responsive design approach ensures your website adapts automatically to different screen sizes, delivering an optimal user experience for all visitors, regardless of their device.")}
        </div>
    </div>
</div>