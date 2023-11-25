document.addEventListener("DOMContentLoaded", function() {
    const canvas = document.getElementById('flowersCanvas');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  
    const flowers = [];
  
    function Flower(x, y) {
      this.x = x;
      this.y = y;
      this.radius = Math.random() * 10 + 5;
      this.color = `hsl(${Math.random() * 360}, 20%, 50%)`; // Muted colors
      this.growthSpeed = Math.random() * 2 + 1;
    }
  
    Flower.prototype.draw = function() {
      ctx.fillStyle = this.color;
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
      ctx.fill();
    };
  
    Flower.prototype.update = function() {
      this.y -= this.growthSpeed;
  
      if (this.radius < 30) {
        this.radius += 0.5;
      }
  
      this.draw();
    };
  
    function createFlower() {
      const x = Math.random() * canvas.width;
      const y = canvas.height + 100;
      flowers.push(new Flower(x, y));
    }
  
    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
  
      flowers.forEach((flower, index) => {
        flower.update();
        if (flower.y + flower.radius < 0) {
          flowers.splice(index, 1);
          createFlower();
        }
      });
  
      requestAnimationFrame(animate);
    }
  
    setInterval(createFlower, 200);
    animate();
  });
