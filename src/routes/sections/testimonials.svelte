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
        {@render Card('test_person.avif', "Sarah Jones", "Manager", "My tech stack mirrors the vibrant diversity of the web itself. From the core languages of HTML5, CSS3, and JavaScript to an arsenal of design tools like Adobe Creative Suite and Sketch, I stay well-equipped. However, I believe in constantly pushing the boundaries, exploring emerging technologies and design trends to ensure my work remains both timeless and cutting-edg")}
        {@render Card('text_person2.avif', "Sarah Jones", "Manager", "My tech stack mirrors the vibrant diversity of the web itself. From the core languages of HTML5, CSS3, and JavaScript to an arsenal of design tools like Adobe Creative Suite and Sketch, I stay well-equipped. However, I believe in constantly pushing the boundaries, exploring emerging technologies and design trends to ensure my work remains both timeless and cutting-edg")}
        {@render Card('test_person2.avif', "Sarah Jones", "Manager", "My tech stack mirrors the vibrant diversity of the web itself. From the core languages of HTML5, CSS3, and JavaScript to an arsenal of design tools like Adobe Creative Suite and Sketch, I stay well-equipped. However, I believe in constantly pushing the boundaries, exploring emerging technologies and design trends to ensure my work remains both timeless and cutting-edg")}

    </Carousel>
    

</div>