
<script lang='ts'>
  // peacoq_1080p
  import { onMount, onDestroy } from 'svelte';
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';

  const width = writable(0);
  const height = writable(0);
  const video_width = writable(0);
  const video_top = writable(0);
  const video_left = writable(0);

  let keydownHandler: (event: KeyboardEvent) => void;

  onMount(() => {
    width.set(window.innerWidth);
    height.set(window.innerHeight);

    video_width.set(Math.floor(1 * window.innerWidth))
    video_top.set(Math.floor(0 * window.innerWidth))
    video_left.set(Math.floor(0 * window.innerWidth))


    const video = document.getElementById('myVideo');
    video.play();

    keydownHandler = async function(event) {
      // Define an async function
      const navigate = async (url: string, imgSrc: string) => {
        const img = new Image();
        img.src = imgSrc;
        img.onload = async () => {
          await goto(url);
        };
      }
      //Check if the pressed key is the left arrow key
      if (event.key === 'ArrowLeft' || event.key === 'PageUp') {
        // Navigate to the desired URL when the left arrow key is pressed
        navigate('/slide_133', '/slides_png/slide_133.png');
      }
      //Check if the pressed key is the right arrow key
      else if (event.key === 'ArrowRight' || event.key === 'PageDown') {
        // Navigate to the desired URL when the right arrow key is pressed
        navigate('/slide_135', '/slides_png/slide_135.png');
      }
    };

    document.addEventListener('keydown', keydownHandler);
  });

  onDestroy(() => {
    if (typeof window !== 'undefined') {
      document.removeEventListener('keydown', keydownHandler);
    }
  });
</script>

<div id="floating-number">134</div>
<video id="myVideo" style="position:absolute; top:{$video_top}px; left:{$video_left}px; width:{$video_width}px;" src="/slides_videos/peacoq_1080p.mp4" muted playsinline></video>
<img src="/slides_png/slide_134.png" alt="slide_134" width="{$width}">

              
