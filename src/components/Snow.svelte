<script>
	import P5 from './P5.svelte';
	const sketch = (p5, target) => {
		const snowflakes = [];
		function snowflake() {
			// initialize coordinates
			this.posX = 0;
			this.posY = p5.random(-50, 0);
			this.initialangle = p5.random(0, 2 * p5.PI);
			this.size = p5.random(2, 5);

			// radius of snowflake spiral
			// chosen so the snowflakes are uniformly spread out in area
			this.radius = p5.sqrt(p5.random(p5.pow(p5.width / 2, 2)));

			this.update = function (time) {
				// x position follows a circle
				let w = 0.6; // angular speed
				let angle = w * time + this.initialangle;
				this.posX = p5.width / 2 + this.radius * p5.sin(angle);

				// different size snowflakes fall at slightly different y speeds
				this.posY += p5.pow(this.size, 0.5);

				// delete snowflake if past end of screen
				if (this.posY > p5.height) {
					let index = snowflakes.indexOf(this);
					snowflakes.splice(index, 1);
				}
			};

			this.display = function () {
				p5.ellipse(this.posX, this.posY, this.size);
			};
		}

		p5.setup = () => {
			const { width, height } = target.getBoundingClientRect();
			console.log({ height });
			p5.createCanvas(width, height);
			p5.fill(240);
			p5.noStroke();
		};
		p5.draw = () => {
			p5.background('#1F005F');
			let t = p5.frameCount / 60; // update time

			// create a random number of snowflakes each frame
			for (let i = 0; i < p5.random(5); i++) {
				snowflakes.push(new snowflake()); // append snowflake object
			}

			// loop through snowflakes with a for..of loop
			for (let flake of snowflakes) {
				flake.update(t); // update snowflake position
				flake.display(); // draw snowflake
			}
		};
		p5.windowResized = () => {
			const { width, height } = target.getBoundingClientRect();
			p5.resizeCanvas(width, height);
		};
	};
</script>

<P5 {sketch} />
