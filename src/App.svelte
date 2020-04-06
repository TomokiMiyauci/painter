<script>
	let isDrag = false
	
	const hand = () => {
		isDrag = true
	}


	const clear = () => {
		const canvas = document.querySelector('#draw-area');
		const context = canvas.getContext('2d');
  		context.clearRect(0, 0, canvas.width, canvas.height);
	}

	const l = (event) => {		
		isDrag = false
		lastPosition.x = null
		lastPosition.y = null
	}

	const getContext = () => {
		return document.querySelector('#draw-area').getContext('2d'); 
	}

	const handleMousemove = (event) => {
		draw(event.layerX, event.layerY)
	}

	const lastPosition = { x: null, y: null };

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
	div { width: 100%; height: 100%; }
</style>

<div>
	<canvas
		on:mousedown={hand}
		on:mouseup={l}
		on:mouseout={l}
		on:mousemove={handleMousemove}
		id="draw-area"
		width="600px"
		height="600px"
		style="border: 1px solid #000000;">
	</canvas>
	<button on:click={clear}></button>
</div>
<!-- <div on:mousemove={handleMousemove}>
	The mouse position is {m.x} x {m.y}
</div> -->