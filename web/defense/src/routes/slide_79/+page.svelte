
<script lang='ts'>
  // protocols_high_loss
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

    video_width.set(Math.floor(0.92 * window.innerWidth))
    video_top.set(Math.floor(0.285 * window.innerWidth))
    video_left.set(Math.floor(0.03 * window.innerWidth))


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
        navigate('/slide_78', '/slides_png/slide_78.png');
      }
      //Check if the pressed key is the right arrow key
      else if (event.key === 'ArrowRight' || event.key === 'PageDown') {
        // Navigate to the desired URL when the right arrow key is pressed
        navigate('/slide_80', '/slides_png/slide_80.png');
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

<video id="myVideo" style="position:absolute; top:{$video_top}px; left:{$video_left}px; width:{$video_width}px;" src="/slides_videos/protocols_high_loss.mp4" muted playsinline></video>
<img src="/slides_png/slide_79.png" alt="slide_79" width="{$width}">

              
