<script>
  import Drawer from "./Drawer.svelte";
  import { __DEV__ } from "./config";
	let run = true;
  let drawerSize = {
    height: ~~window.innerHeight,
    width: ~~window.innerWidth
  };

  let pallete = new Array(drawerSize.height * drawerSize.width).fill(0);

  const generate = () => {
    if (__DEV__) {
      console.time();
    }

    pallete = pallete.map(() => [
      Math.random() * 255,
      Math.random() * 255,
      Math.random() * 255
    ]);

    if (__DEV__) {
      console.timeEnd();
    }
  };

  const anim = () => {
		generate();
		if (run) {
			requestAnimationFrame(anim);
		}
	};
	anim();

  const stop = () => run = false;
</script>

<style>
  :global(body) {
    padding: 0;
    overflow: hidden;
  }

  .generate {
    position: fixed;
    opacity: 0.3;
  }
</style>

<button class="generate" on:click={stop}>stop</button>
<Drawer {...drawerSize} {pallete} />
