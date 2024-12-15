<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spider Web</title>
    <style>
        body {
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #121212;
        }
        canvas {
            display: block;
            background-color: #1a1a1a;
            border: 2px solid #ffffff;
        }
    </style>
</head>
<body>
    <canvas id="spiderWeb"></canvas>

    <script>
        const canvas = document.getElementById("spiderWeb");
        const ctx = canvas.getContext("2d");

        // Set canvas size
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        // Center of the web
        const centerX = canvas.width / 2;
        const centerY = canvas.height / 2;

        // Web settings
        const rings = 10; // Number of concentric circles
        const spokes = 12; // Number of radial lines
        const maxRadius = Math.min(centerX, centerY) - 50; // Radius of the outermost circle

        // Draw concentric circles
        for (let i = 1; i <= rings; i++) {
            const radius = (i / rings) * maxRadius;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, 0, 2 * Math.PI);
            ctx.strokeStyle = "rgba(255, 255, 255, 0.5)";
            ctx.lineWidth = 1;
            ctx.stroke();
        }

        // Draw radial spokes
        for (let i = 0; i < spokes; i++) {
            const angle = (i / spokes) * 2 * Math.PI;
            const endX = centerX + maxRadius * Math.cos(angle);
            const endY = centerY + maxRadius * Math.sin(angle);
            ctx.beginPath();
            ctx.moveTo(centerX, centerY);
            ctx.lineTo(endX, endY);
            ctx.strokeStyle = "rgba(255, 255, 255, 0.5)";
            ctx.lineWidth = 1;
            ctx.stroke();
        }

        // Draw connecting threads
        for (let i = 1; i < rings; i++) {
            const innerRadius = (i / rings) * maxRadius;
            const outerRadius = ((i + 1) / rings) * maxRadius;

            for (let j = 0; j < spokes; j++) {
                const startAngle = (j / spokes) * 2 * Math.PI;
                const endAngle = ((j + 1) / spokes) * 2 * Math.PI;

                const startX = centerX + innerRadius * Math.cos(startAngle);
                const startY = centerY + innerRadius * Math.sin(startAngle);

                const endX = centerX + outerRadius * Math.cos(endAngle);
                const endY = centerY + outerRadius * Math.sin(endAngle);

                ctx.beginPath();
                ctx.moveTo(startX, startY);
                ctx.lineTo(endX, endY);
                ctx.strokeStyle = "rgba(255, 255, 255, 0.3)";
                ctx.lineWidth = 0.8;
                ctx.stroke();
            }
        }
    </script>
</body>
</html>
