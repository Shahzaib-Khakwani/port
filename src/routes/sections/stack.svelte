<script>
    import Card from "$lib/components/tapToFlipCard.svelte"
    import { gsap } from "gsap";
    import { onMount } from "svelte";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    gsap.registerPlugin(ScrollTrigger);

    onMount(() => {
        const boxes = document.querySelectorAll(".stackBox");
        
        boxes.forEach((box) => {
            ScrollTrigger.create({
                trigger: box,
                start: "top bottom-=100",  
                end: "bottom top+=100",    
                onEnter: () => gsap.to(box, { scale: 1.1, duration: 0.5, ease: "power1.out" }),
                onLeave: () => gsap.to(box, { scale: 1, duration: 0.5, ease: "power1.in" }),
                onEnterBack: () => gsap.to(box, { scale: 1.1, duration: 0.5, ease: "power1.out" }),
                onLeaveBack: () => gsap.to(box, { scale: 1, duration: 0.5, ease: "power1.in" }),
                markers: false
            });
        });

        gsap.from('.stackCube', {
          scale: 0.5,
          duration: 0.8, // 0.8 seconds, not 800 seconds
          scrollTrigger: {
            trigger: '#stack',
            start: "top center",  
            end: "bottom-=300 bottom",
            pin: ".stackSection",
            scrub:true, 
            markers: false
          }
        })

        const cursor = document.createElement('div');
        cursor.classList.add('stack-cursor');
        cursor.innerHTML = `
          <div class="stack-cursor-circle rounded-3xl">
            <span class='font-public p-8'>Tap to Flip</span>
          </div>
        `;
        document.body.appendChild(cursor);

        const style = document.createElement('style');
        style.textContent = `
          .stack-cursor {
            position: fixed;
            width: 200px;
            height: 50px;
            pointer-events: none;
            z-index: 9999;
            opacity: 0;
            transition: transform 0.1s ease, opacity 0.2s ease;
            transform: translate(-50%, -50%) scale(0.4);
          }
          
          .stack-cursor-circle {
            width: 100%;
            height: 100%;
            background-color: white;
            display: flex;
            align-items: center;
            justify-content: center;
          }
          
          .stack-cursor-circle span {
            font-family: sans-serif;
            font-weight: 600;
            font-size: 20px;
            color: #333;
          }
          
          .project-card-hover {
            cursor: none !important;
          }
        `;
        document.head.appendChild(style);
        
        const stackCards = document.querySelectorAll('.stackBox');
        
        stackCards.forEach(card => {
            card.classList.add('project-card-hover');
            
            card.addEventListener('mouseenter', () => {
                cursor.style.opacity = '1';
                cursor.style.transform = 'translate(-50%, -50%) scale(1)';
            });
            
            card.addEventListener('mouseleave', () => {
                cursor.style.opacity = '0';
                cursor.style.transform = 'translate(-50%, -50%) scale(0.8)';
            });
            
            card.addEventListener('mousemove', (e) => {
                cursor.style.left = `${e.clientX}px`;
                cursor.style.top = `${e.clientY}px`;
            });
        });
    });
</script>

<div class="min-h-screen w-full relative overflow-hidden">


<div class="stackSection h-screen w-full absolute top-0 left-0 bg-transparent z-10">
  <div class="relative h-screen w-full">
      <img class="stackCube w-3/4 absolute top-[10vh] lg:top-1/3 left-1/2 transform -translate-x-1/2 -translate-y-1/2 " 
      src="stack_cube.avif" 
      alt="">
  </div>
</div>
<div id='stack' class=" min-h-screen w-full my-16 px-16 relative grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-y-16 gap-x-4 justify-items-center">

    


    <div class="z-20 col-span-1 md:col-span-2 lg:col-span-3 h-auto p-4">
        <h1 class="font-public text-[38px] text-center font-medium">
            My Stack
        </h1>
    </div>

    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="django.png" title='Django'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Svelte.png" title='Svelte'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="compose.png" title='Docker'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Celery.png" title='Celery'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="node.png" title='Node'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo='postgres.png' title='PostgreSql'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="redis.png" title='Redis'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Sanity.png" title='Sanity'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="gsap.png" title='Gsap'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Python.png" title='Flask'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Pandas.png" title='Pandas'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Anaconda.png" title='Anaconda'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="Flask.png" title='Flask'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="NumPy.png" title='Numpy'/></div>
    <div  class="z-20 stackBox transform-gpu transition-transform"><Card logo="TensorFlow.png" title='Tensorflow'/></div>


</div>
</div>
