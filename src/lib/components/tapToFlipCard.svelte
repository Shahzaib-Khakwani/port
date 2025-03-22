<script>
  export let logo = "mailchimp.png"; 
  export let logoAlt = "Slack logo";
  export let title = "Mail Chimp";
  export let description = "Team communication platform";

  export let width = "w-56 sm:w-80 md:w-96";
  export let height = "h-56 sm:h-80 md:h-96";
</script>
<div class="font-public">
  <label class={`block ${width} ${height} cursor-pointer`}>
    <input type="checkbox" class="hidden" />
    <div class="relative w-full h-full text-center transition-transform duration-500 shadow-lg rounded-lg sm:rounded-xl md:rounded-2xl" style="transform-style: preserve-3d">
      <!-- Front face with transparent backdrop blur effect -->
      <div class="absolute inset-0 w-full h-full rounded-lg sm:rounded-xl md:rounded-2xl flex flex-col justify-center items-center bg-transparent bg-opacity-30 border border-white/30 backdrop-blur-md shadow-lg" style="backface-visibility: hidden">
        <div class="flex flex-col items-center gap-2 sm:gap-3 md:gap-5 p-2 sm:p-3 md:p-4">
          <img src={logo} alt={logoAlt} class="w-24 h-24 sm:w-32 sm:h-32 md:w-40 md:h-40 lg:w-48 lg:h-48 object-contain" />
          <h2 class="text-lg sm:text-xl md:text-2xl font-medium m-0 text-black/80">{title}</h2>
        </div>
      </div>
      <!-- Back face with transparent backdrop blur effect -->
      <div class="absolute inset-0 w-full h-full rounded-lg sm:rounded-xl md:rounded-2xl flex flex-col justify-center items-center bg-transparent bg-opacity-30 p-3 sm:p-4 md:p-5 border border-white/30 backdrop-blur-md shadow-lg" style="backface-visibility: hidden; transform: rotateY(180deg)">
        <h1 class="text-lg sm:text-xl md:text-2xl mb-2 md:mb-3 text-black/80">{title}</h1>
        <p class="text-sm sm:text-base overflow-y-auto max-h-[60%] text-black/70">{description}</p>
      </div>
    </div>
  </label>
</div>

<style>
  input:checked + div {
    transform: rotateY(180deg);
  }
</style>