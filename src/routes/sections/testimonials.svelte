<script>
    import Carousel from '$lib/components/carousel.svelte';
    import { render } from 'svelte/server';


</script>

{#snippet Card(image, name, title, reviews)}
<div class="w-full flex justify-center items-center">
	<div class="w-full md:w-5/6 flex flex-col rounded-3xl p-4 md:p-8 justify-center items-center bg-[#FFFFFF]">
		<div class="flex flex-col justify-center items-center">
            <div>
                <img src={image} class="w-16 h-16 md:w-24 md:h-24" alt={name} />
            </div>
            <h1 class="text-xl md:text-[28px] font-medium text-center">{name}</h1>
            <h3 class="text-xs md:text-[14px] text-black/40 font-medium text-center">{title}</h3>
        </div>
        <p class="w-full md:w-3/4 text-center leading-6 md:leading-8 mt-4 md:mt-8 text-[#4d4d4d] text-sm md:text-[20px] italic font-public line-clamp-4 md:line-clamp-none overflow-hidden">
            {reviews}
        </p>
        <button class="mt-2 text-[#F94706] text-xs md:hidden">Read more</button>
    </div>
</div>
{/snippet}



<div class="min-h-screen  w-full flex flex-col justify-center items-center bg-[#FFFFFF]">
    <h1  class="text-[38px] text-center  font-public font-medium mb-4">
        Kind Words From Clients
    </h1>
    <Carousel  perPage={1} autoplay="2000">
        {@render Card('test_person2.avif', "Aun Haider", "Manager", "A social media app built with Django and PostgreSQL, containerized with Docker. Redis powers caching and Celery handles background tasks, with Celery Beat for scheduling. Kafka enables real-time event streaming for scalability.")}



        {@render Card('test_person2.avif', "Hassan Ali Sajid", "Manager", "The frontend website for the robotics company is designed to showcase its innovations, products, and services. Built for performance and user experience, it features an intuitive interface, interactive elements, and a modern design. The site highlights the company's expertise in robotics, providing detailed insights into its technology, applications, and industry impact.")}


        {@render Card('test_person2.avif', "Shehryar", "Manager", "A social media app with a Flutter frontend and a Django-PostgreSQL backend, containerized with Docker. Redis handles caching, Celery manages background tasks, and Kafka enables real-time event streaming. The app also includes a carpooling feature.")}

    </Carousel>
    

</div>