<!--
@component
PhotoSlide.svelte — A full-bleed photo slide with a gradient caption overlay.

Renders an image that fills the viewport with object-fit: cover. A gradient
overlay at the bottom displays the title, caption, and photo credit.

USAGE EXAMPLE:
<PhotoSlide photo={{
  filename: 'subway-platform.jpg',
  title: 'Waiting for the L\',
  caption: 'Commuters line the platform at Bedford Avenue during morning rush.',
  credit: 'Photo by Jane Doe'
}} />
-->
<script>
  import { base } from '$app/paths';

  let {
    photo, // Object with filename, title, caption, date, and credit
  } = $props();
</script>

<div class="slide" data-slide data-photo>
  <img src={`${base}/photos/${photo.filename}`} alt={photo.title} />
  <div class="caption">
    <div class="caption-inner">
      <h2>{photo.title}</h2>
      <p>{photo.caption}</p>
      {#if photo.date}
        <span class="date">{photo.date}</span>
      {/if}
      <span class="credit">{photo.credit}</span>
    </div>
  </div>
</div>

<style lang="scss">
  .slide {
    height: 100%;
    flex: 0 0 100%;
    position: relative;
    background: var(--color-blossom-light, #fce4ec); // soft fallback

    @container (min-width: 768px) {
      display: flex;
    }
  }

  .slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;

    @container (min-width: 768px) {
      width: 60%;
      flex-shrink: 0;
    }
  }

  .caption {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 2rem 1.5rem 3.5rem;
    border-top: 2px solid var(--color-blossom-medium, #f48fb1); // minimal accent
    background: linear-gradient(
      to top,
      rgba(0, 0, 0, 0.82) 0%,
      rgba(0, 0, 0, 0.38) 68%,
      transparent 100%
    );
    color: white;

    @container (min-width: 768px) {
      position: static;
      width: 40%;
      display: flex;
      align-items: center;
      padding: 3rem;
      border-top: 0;
      border-left: 3px solid var(--color-blossom-medium, #f48fb1);
      background: color-mix(in srgb, var(--color-blossom-light, #fce4ec) 14%, black);
    }
  }

  .caption-inner {
    max-width: 600px;
  }

  .caption h2 {
    margin: 0 0 0.5rem;
    padding-left: 0.6rem;
    border-left: 2px solid var(--color-blossom-accent, #ec407a); // tiny title accent
    font-size: 1.25rem;
    line-height: 1.3;
    color: white;

    @container (min-width: 768px) {
      font-size: 1.75rem;
      margin-bottom: 1rem;
    }
  }

  .caption p {
    margin: 0 0 0.5rem;
    font-size: 0.9375rem;
    line-height: 1.5;
    opacity: 0.92;

    @container (min-width: 768px) {
      font-size: 1.0625rem;
      line-height: 1.7;
      margin-bottom: 1.5rem;
    }
  }

  .caption .date {
    display: block;
    margin-bottom: 0.2rem;
    font-size: 0.75rem;
    color: color-mix(in srgb, white 75%, var(--color-blossom-light, #fce4ec));

    @container (min-width: 768px) {
      font-size: 0.8125rem;
      margin-bottom: 0.35rem;
    }
  }

  .caption .credit {
    font-size: 0.75rem;
    opacity: 0.7;

    @container (min-width: 768px) {
      font-size: 0.8125rem;
    }
  }

    @media (max-width: 767px) {
    .caption {
      background: rgba(255, 255, 255, 0.30);
      backdrop-filter: blur(6px);
      -webkit-backdrop-filter: blur(6px);
      color: #222;
      border-top-color: var(--color-blossom-light, #fce4ec);
    }

    .caption h2,
    .caption p,
    .caption .date,
    .caption .credit {
      color: #222;
    }
  }
</style>
