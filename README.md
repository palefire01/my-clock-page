<!DOCTYPE html>
<html lang="de">

<head>
    <meta charset="utf-8">
    <title>title</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://efpage.de/DML/DML_homepage/lib/DML-min.js"></script>
    <style>
        #clockContainer {
            width: 200px;  /* Adjust as needed */
            height: 200px; /* Adjust as needed */
            position: relative;
            border: 7px solid #282828;
            border-radius: 50%; 
            margin: 50px;
            box-shadow: -4px -4px 10px rgba(67,67,67,0.5), inset 4px 4px 10px rgba(0,0,0,0.5),
            inset -4px -4px 10px rgba(67,67,67,0.5), 4px 4px 10px rgba(0,0,0,0.3);
        }

        #clockCanvas {
            position: absolute;
            top: 0;
            left: 0;
            z-index: 2; /* ensure it's above the background */
        }

        #clockBackground {
            width: 100%;
            height: 100%;
            background-image: url('https://media.newyorker.com/photos/5ea9ff8878fed0000976e370/master/w_1920,c_limit/200511_r36409web.gif'); /* Replace with your image path */
            background-size: cover;
            background-position: center;
            border-radius: 50%;
        }
    </style>
</head>

<body>
    <div id="clockContainer">
        <canvas id="clockCanvas"></canvas>
        <div id="clockBackground"></div>
    </div>
    <script>
        "use strict";
        const cx = 100, cy = 100;  // Radius

        let canvasElem = document.getElementById("clockCanvas");
        canvasElem.width = 2 * cx;
        canvasElem.height = 2 * cy;
        let c = canvasElem.getContext("2d");
        c.lineCap = "round";

        function tick(color, width, angle, length, innerlength = 0) {
            function ls(length) { return length * Math.sin(angle / 180.0 * Math.PI) }
            function lc(length) { return -length * Math.cos(angle / 180.0 * Math.PI) }
            c.strokeStyle = color;
            c.lineWidth = width;
            c.beginPath();
            c.moveTo(cx + ls(innerlength), cy + lc(innerlength));
            c.lineTo(cx + ls(length), cy + lc(length));
            c.stroke();
        }

        function drawClock() {
            c.clearRect(0, 0, canvasElem.width, canvasElem.height);  // Clear the canvas
            for (let i = 0; i < 360; i += 30) {
                if ((i % 90) == 0) tick("#1df52f", 5, i, 88, 70);
                else tick("#bdbdcb", 3, i, 88, 75);
            }
            
            let t = new Date();
            tick("#61afff", 5, t.getHours() * 30, 50);
            tick("#71afff", 2, t.getMinutes() * 6, 70);
            tick("#ee791a", 2, t.getSeconds() * 6, 80);

            c.fillStyle = "#4d4b63";
            c.beginPath();
            c.arc(cx, cy, 10, 0, 2 * Math.PI, false);
            c.fill();
        }
        drawClock();
        setInterval(drawClock, 1000);
    </script>
</body>

</html>
