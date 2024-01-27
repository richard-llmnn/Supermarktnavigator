<script lang="ts">
	import { onMount } from 'svelte';
	let svg: SVGSVGElement;
	onMount(() => {
		svg.addEventListener('mousedown', startDrag);
		svg.addEventListener('mousemove', drag);
		svg.addEventListener('mouseup', endDrag);

		function getMousePosition(evt) {
			var CTM = svg.getScreenCTM();
			if (CTM === null) return;
			return {
				x: (evt.clientX - CTM.e) / CTM.a,
				y: (evt.clientY - CTM.f) / CTM.d
			};
		}

		var selectedElement: HTMLElement, offset;

		function startDrag(evt) {
			if (evt.target.classList.contains('draggable')) {
				selectedElement = evt.target;
				offset = getMousePosition(evt);
				offset.x -= parseFloat(selectedElement.getAttributeNS(null, 'x'));
				offset.y -= parseFloat(selectedElement.getAttributeNS(null, 'y'));
			}
		}

		function drag(evt) {
			if (selectedElement) {
				var coord = getMousePosition(evt);
				console.log(selectedElement.getBoundingClientRect().width);
				let w = parseInt(selectedElement.width.baseVal.value);
				let h = parseInt(selectedElement.height.baseVal.value);
				let x = coord.x - offset.x;
				let y = coord.y - offset.y;
				selectedElement.setAttributeNS(null, 'y', y);
				selectedElement.setAttributeNS(null, 'x', x);
				//if (y > 0.5 && (y + h) < 19.5) selectedElement.setAttributeNS(null, "y", y)
				//if (x > 0.5 && (x + w) < 29.5) selectedElement.setAttributeNS(null, "x", x)
			}
		}

		function endDrag(evt) {
			selectedElement = null;
		}
	});
</script>

<svg xmlns="http://www.w3.org/2000/svg" bind:this={svg} viewBox="0 0 30 20">
	<style>
		.background {
			fill: #eee;
		}
		.static {
			cursor: not-allowed;
		}
		.draggable {
			cursor: move;
		}
	</style>

	<rect x="0" y="0" width="30" height="20" class="background" />
	<rect class="draggable" x="4" y="5" width="8" height="10" fill="#007bff" />
	<rect class="draggable" x="18" y="5" width="8" height="10" fill="#888" />
</svg>

<div width="30px" height="20px" style="background: green">delete</div>
