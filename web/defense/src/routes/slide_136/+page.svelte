
<script lang='ts'>
  import { onMount, onDestroy } from 'svelte';
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';
  import PeacoqPulseOverlap from '$lib/peacoq_pulse_overlap.svelte';

  const width = writable(0);
  const height = writable(0);
  onMount(() => {
    width.set(window.innerWidth);
    height.set(window.innerHeight);
  });
</script>

<div id="floating-number">136</div>
<PeacoqPulseOverlap prev_slide='/slide_135' next_slide='/slide_137'/>
<img src="/slides_png/slide_136.png" alt="slide_136" width="{$width}" style="top: 0px; position: absolute; z-index: -1;">
              
