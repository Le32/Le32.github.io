<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Heart Blast Animation</title>
    <style>
        body {
            background-color: black;
            color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            position: relative;
            font-family: Arial, sans-serif;
        }

        .heart-button {
            width: 100px;
            height: 100px;
            background-color: red;
            border: none;
            border-radius: 50px 50px 0 0;
            position: relative;
            cursor: pointer;
            outline: none;
            transition: transform 0.3s;
            transform: scale(1);
            margin: 0;
            padding: 0;
        }

        .heart-button:before,
        .heart-button:after {
            content: '';
            width: 100px;
            height: 100px;
            background-color: red;
            border-radius: 50px;
            position: absolute;
            top: -50px;
        }

        .heart-button:before {
            left: 0;
        }

        .heart-button:after {
            left: 50px;
        }

        #message {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 36px; /* Increased font size for visibility */
            font-weight: bold;
            color: pink; /* Changed to pink for better contrast */
            text-align: center;
            opacity: 0; /* Initially hidden */
            transition: opacity 1s; /* Smooth transition */
        }

        .heart-rain {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            overflow: hidden;
            pointer-events: none;
        }

        .heart {
            position: absolute;
            background-color: red;
            width: 30px; /* Increased heart size */
            height: 30px; /* Increased heart size */
            border-radius: 50%; /* Perfect circle */
            opacity: 0.8;
            animation: fall linear infinite;
        }

        @keyframes fall {
            to {
                transform: translateY(100vh);
            }
        }

        @keyframes blast {
            0% {
                transform: scale(1);
                opacity: 1;
            }
            100% {
                transform: scale(5); /* Bigger blast */
                opacity: 0;
            }
        }
    </style>
</head>
<body>

    <button class="heart-button" onclick="startAnimation()"></button>
    <div id="message">Love you to my Meow Meow</div>
    <div class="heart-rain" id="heartRain"></div>

    <script>
        function startAnimation() {
            // Show the message
            const message = document.getElementById('message');
            message.style.display = 'block';
            message.style.opacity = 1; // Fade in the message

            // Change background color
            document.body.style.transition = 'background-color 1s';
            document.body.style.backgroundColor = 'pink';

            // Create heart blast effect
            blastHearts();

            // Create heart rain effect
            createHeartRain();
        }

        function blastHearts() {
            const heartBlast = document.createElement('div');
            heartBlast.style.position = 'absolute';
            heartBlast.style.top = '50%';
            heartBlast.style.left = '50%';
            heartBlast.style.transform = 'translate(-50%, -50%)';
            heartBlast.style.backgroundColor = 'red';
            heartBlast.style.width = '200px'; // Bigger blast
            heartBlast.style.height = '200px'; // Bigger blast
            heartBlast.style.borderRadius = '50%';
            heartBlast.style.animation = 'blast 0.5s forwards'; // Blast animation

            document.body.appendChild(heartBlast);

            // Remove the blast after animation
            heartBlast.addEventListener('animationend', () => {
                heartBlast.remove();
            });
        }

        function createHeartRain() {
            for (let i = 0; i < 30; i++) {
                createHeart();
            }
        }

        function createHeart() {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = Math.random() * 2 + 3 + 's'; // Random fall duration
            heart.style.animationDelay = Math.random() * 2 + 's'; // Random delay before falling
            document.getElementById('heartRain').appendChild(heart);

            // Remove heart after animation
            heart.addEventListener('animationend', () => {
                heart.remove();
            });
        }
    </script>

</body>
</html>
