
<script lang='ts'>
  import { onMount, onDestroy } from 'svelte';
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';

  const width = writable(0);
  const height = writable(0);

  let keydownHandler: (event: KeyboardEvent) => void;

  onMount(() => {
    width.set(window.innerWidth);
    height.set(window.innerHeight);

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
        navigate('/slide_134', '/slides_png/slide_134.png');
      }
      //Check if the pressed key is the right arrow key
      else if (event.key === 'ArrowRight' || event.key === 'PageDown') {
        // Navigate to the desired URL when the right arrow key is pressed
        navigate('/slide_136', '/slides_png/slide_136.png');
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

<div id="floating-number">135</div>
<img src="/slides_png/slide_135.png" alt="slide_135" width="{$width}">
              
