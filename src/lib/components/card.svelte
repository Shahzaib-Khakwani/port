<script>
    let { text } = $props();
</script>

<div class="w-full">
    <div class="h-full bg-white/30 border-4 md:border-8 border-[#EFF0FF] backdrop-blur-3xl p-2 md:p-4 rounded-xl md:rounded-3xl">
        <p class="text-center text-[#4d4d4d] text-base sm:text-lg md:text-[24px] font-public font-normal leading-tight md:leading-relaxed bg-white w-full h-full rounded-xl md:rounded-3xl p-3 sm:p-4 md:p-8">
            {text}
        </p>
    </div>
</div>