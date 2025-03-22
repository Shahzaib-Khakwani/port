<script>
    import { onMount } from 'svelte';
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger";

    gsap.registerPlugin(ScrollTrigger);

    let projectCards = [];
    let cursor;
  
    onMount(() => {

      const projectBoxes = document.querySelectorAll(".projectBox")

      projectBoxes.forEach((box)=>{
        ScrollTrigger.create({
          trigger:box,
          start: "top bottom-=100",  
          end: "bottom top+=100",    
          onEnter: () => gsap.from(box, { scale: 0.8, duration: 0.4, ease: "power1.out" }),
          onLeave: () => gsap.to(box, { scale: 1, duration: 0.5, ease: "power1.in" }),
          onEnterBack: () => gsap.from(box, { scale: 0.8, duration: 0.4, ease: "power1.out" }),
          onLeaveBack: () => gsap.to(box, { scale: 1, duration: 0.5, ease: "power1.in" }),
          markers: false
        })
      })






      cursor = document.createElement('div');
      cursor.classList.add('custom-cursor');
      cursor.innerHTML = `
        <div class="cursor-circle rounded-3xl">
          <span class='font-public p-8'>View Project</span>
        </div>
      `;
      document.body.appendChild(cursor);
  
      const style = document.createElement('style');
      style.textContent = `
        .custom-cursor {
          position: fixed;
          width: 200px;
          height: 50px;
          pointer-events: none;
          z-index: 9999;
          opacity: 0;
          transition: transform 0.1s ease, opacity 0.2s ease;
          transform: translate(-50%, -50%) scale(0.4);
        }
        
        .cursor-circle {
          width: 100%;
          height: 100%;
          background-color: white;
          display: flex;
          align-items: center;
          justify-content: center;
        }
        
        .cursor-circle span {
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
      
      projectCards = document.querySelectorAll('.project-card');
      
      projectCards.forEach(card => {
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
  
  {#snippet ProjectCard(title, imgSrc)}
  <div class="project-card relative w-full sm:w-5/6 h-60 sm:h-72 md:h-96 rounded-xl sm:rounded-2xl md:rounded-3xl text-center bg-[#F7F8FF] backdrop-blur-3xl">
    <div class="flex justify-center items-center w-[90%] h-[90%] bg-white rounded-xl sm:rounded-2xl md:rounded-3xl absolute left-1/2 top-1/2 transform -translate-x-1/2 -translate-y-1/2 overflow-hidden">
      <div class="relative w-full h-full group">
        <img
          class="w-full h-auto object-contain rounded-xl sm:rounded-2xl md:rounded-3xl shadow-md transition-transform duration-300 ease-in-out group-hover:scale-110" 
          src={imgSrc}
          alt="">
        <div class="absolute inset-0 bg-gray-800 opacity-0 group-hover:opacity-40 transition-opacity duration-300 ease-in-out rounded-xl sm:rounded-2xl md:rounded-3xl"></div>
      </div>
    </div>
  </div>
  <h3 class="mt-2 sm:mt-3 md:mt-4 text-lg sm:text-xl md:text-2xl lg:text-[28px] text-center text-black font-public font-semibold w-full sm:w-4/5">{title}</h3>
{/snippet}
  
  <div class="min-h-screen max-w-7xl mb-16 mx-auto grid grid-cols-1 md:grid-cols-1 lg:grid-cols-2 gap-y-16 gap-x-4 justify-items-center">
    <div class="col-span-1 md:col-span-1 lg:col-span-2 h-auto p-4">
        <h1 class="font-public text-[38px] text-center font-medium">
            Projects
        </h1>
    </div>
    <div class="projectBox w-full h-full flex flex-col items-center justify-center my-4">{@render ProjectCard("Specialised Web App","https://framerusercontent.com/images/HowmrQKMjv4J2RQAp5h9XISrO0E.jpg?scale-down-to=1024")}</div>
    <div class="projectBox w-full h-full flex flex-col items-center justify-center my-4">{@render ProjectCard("Specialised Web App","https://framerusercontent.com/images/HowmrQKMjv4J2RQAp5h9XISrO0E.jpg?scale-down-to=1024")}</div>
    <div class="projectBox w-full h-full flex flex-col items-center justify-center my-4">{@render ProjectCard("Specialised Web App","https://framerusercontent.com/images/HowmrQKMjv4J2RQAp5h9XISrO0E.jpg?scale-down-to=1024")}</div>
    <div class="projectBox w-full h-full flex flex-col items-center justify-center my-4">{@render ProjectCard("Specialised Web App","https://framerusercontent.com/images/HowmrQKMjv4J2RQAp5h9XISrO0E.jpg?scale-down-to=1024")}</div>
    
  </div>