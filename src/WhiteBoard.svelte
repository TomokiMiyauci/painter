<script>
  import { onMount } from 'svelte';

	let isDrag = false
	const lastPosition = { x: null, y: null };

	const drawOn = () => {
    context.beginPath();
		isDrag = true
  }

  const drawOff = (event) => {
    context.closePath();
    isDrag = false
    lastPosition.x = null
    lastPosition.y = null
  }

  let canvas
  let context

  onMount(() => {
    canvas =  document.querySelector('#draw-area');
    context = canvas.getContext('2d');
  })

	const clear = () => {
  		context.clearRect(0, 0, canvas.width, canvas.height);
	}

	const handleMousemove = (event) => {
		draw(event.layerX, event.layerY)
	}


	const draw = (x, y) => {
		if(!isDrag) {
			return;
		}
		const canvas = document.querySelector('#draw-area');
		const context = canvas.getContext('2d');

		const currentColor = '#000000'
		context.lineCap = 'round';
		context.lineJoin = 'round';
		context.lineWidth = 5;
		context.strokeStyle = currentColor;
		if (lastPosition.x === null || lastPosition.y === null) {
		context.moveTo(x, y);
		} else {
		context.moveTo(lastPosition.x, lastPosition.y);
		}
		context.lineTo(x, y);
		context.stroke();

		lastPosition.x = x;
		lastPosition.y = y;
	}
</script>

<style>
  canvas {
    border: 1px solid grey;
    border-radius: 1%;
  }
</style>

<div style="position:relative;">

<canvas
  on:mousedown={drawOn}
  on:mouseup={drawOff}
  on:mouseout={drawOff}
  on:mousemove={handleMousemove}
  id="draw-area"
  width="600px"
  height="600px"
  style="border: 1px solid #000000;">
  </canvas>
  <button style="position: absolute;top:0;" on:click={clear}>clear</button>
  <button style="position: absolute;top:30px;width:50px;height:50px" on:click={clear}>clear</button>
</div>
