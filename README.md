<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Edward Gorey Inspired Treehouse Animation</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #ffffff; /* White background */
        }
        canvas {
            border: 1px solid black;
            background: #ffffff; /* Light gray background */
        }
    </style>
</head>
<body>
    <canvas id="canvas" width="800" height="600"></canvas>
    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        let angle = 0;

        function drawScene() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw the background
            ctx.fillStyle = '#f0f0f0';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            // Draw the tree with Gorey style
            drawTree(400, 400);

            // Draw the treehouse
            drawTreehouse(360, 300);

            // Increment the angle for animation
            angle += 0.01;

            // Request the next frame
            requestAnimationFrame(drawScene);
        }

        function drawTree(x, y) {
            ctx.save();
            ctx.translate(x, y);
            ctx.rotate(Math.sin(angle) * 0.02);

            // Trunk (detailed line work)
            ctx.strokeStyle = '#000000'; // Black for trunk
            ctx.lineWidth = 2;
            ctx.beginPath();
            ctx.moveTo(-20, 0);
            ctx.lineTo(-20, 200);
            ctx.lineTo(20, 200);
            ctx.lineTo(20, 0);
            ctx.stroke();

            // Texture on the trunk
            for (let i = 0; i < 20; i++) {
                ctx.beginPath();
                ctx.moveTo(-20, i * 10);
                ctx.lineTo(20, i * 10);
                ctx.stroke();
            }

            // Branches
            drawBranch(-20, 100, -100, -100);
            drawBranch(20, 100, 100, -100);

            ctx.restore();
        }

        function drawBranch(x1, y1, x2, y2) {
            ctx.beginPath();
            ctx.moveTo(x1, y1);
            ctx.lineTo(x2, y2);
            ctx.stroke();

            // Add smaller branches for a more intricate look
            if (Math.abs(x2 - x1) > 20) {
                drawBranch(x2, y2, x2 + (Math.random() - 0.5) * 100, y2 + (Math.random() - 0.5) * 100);
                drawBranch(x2, y2, x2 + (Math.random() - 0.5) * 100, y2 + (Math.random() - 0.5) * 100);
            }
        }

        function drawTreehouse(x, y) {
            ctx.save();
            ctx.translate(x, y);

            // House body (geometric shapes)
            ctx.fillStyle = '#000000'; // Black for house
            ctx.fillRect(-40, -50, 80, 80);

            // Roof (triangle)
            ctx.beginPath();
            ctx.moveTo(-50, -50);
            ctx.lineTo(0, -100);
            ctx.lineTo(50, -50);
            ctx.closePath();
            ctx.fillStyle = '#000000'; // Black for roof
            ctx.fill();

            // Windows (circles)
            ctx.fillStyle = '#ffffff'; // White for windows
            ctx.beginPath();
            ctx.arc(-20, -30, 10, 0, Math.PI * 2);
            ctx.fill();
            ctx.beginPath();
            ctx.arc(20, -30, 10, 0, Math.PI * 2);
            ctx.fill();

            ctx.restore();
        }

        drawScene();
    </script>
</body>
</html>
