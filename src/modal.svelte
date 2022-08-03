<script>
    import { fade, blur, fly, slide, scale } from "svelte/transition";


    const close = () => {
        isModalOpen = false;
    };


</script>

<style>
.modalWrapper {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
}
.modal {
    background: white;
    border-radius: 15px;
    padding: 3rem;
    margin: 3rem;
}


</style>


<div class="modalWrapper" transition:fade>
    <div class="modal" transistion:fly={{ y: 200 }} >
        <button>Close</button>
        <!-- <slot> -->
            <!-- optional fallback -->
        <!-- </slot> -->
        <slot />

    </div>
</div>

