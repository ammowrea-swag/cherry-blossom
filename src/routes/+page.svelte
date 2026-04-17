<script>
  import SlideGallery from '$lib/components/MultimediaGallery/SlideGallery.svelte';
  import TitleSlide from '$lib/components/MultimediaGallery/TitleSlide.svelte';
  import PhotoSlide from '$lib/components/MultimediaGallery/PhotoSlide.svelte';
  import TextSlide from '$lib/components/MultimediaGallery/TextSlide.svelte';
  import CreditsSlide from '$lib/components/MultimediaGallery/CreditsSlide.svelte';


  let { data } = $props();
</script>

<SlideGallery>
  <TitleSlide
    headline="Washington in Bloom"
    intro="A look at D.C.'s iconic cherry trees and the history of the tidal basin bloom."
  />
    {#each data.story as slide (slide.id)}
    {#if slide.type === 'photo'}
      <PhotoSlide photo={slide} />
    {:else if slide.type === 'text'}
      <TextSlide {slide} />
    {/if}
  {/each}

    <CreditsSlide>
    <h2>About These Photographs</h2>
    <p>
      Photos included in this gallery are courtesy of the Library of Congress, free for personal and commercial use. High-resolution scans are available in the
      <a href="https://www.loc.gov/pictures/search/?q=gordon+parks+harlem&co=fsa" target="_blank">
        Prints &amp; Photographs Division</a>'s digital collection.
    </p>
  </CreditsSlide>
</SlideGallery>