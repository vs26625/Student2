---
toc: true
comments: true
layout: post
title: Husky Sprite Sheet
description: A cute little husky to play with. Reminds me of my dog
type: hacks
courses: { compsci: {week: 6} }
---

<body>
    <div>
        <canvas id="spriteContainer"> <!-- Within the base div is a canvas. An HTML canvas is used only for graphics. It allows the user to access some basic functions related to the image created on the canvas (including animation) -->
            <img id="HuskySpriteSheet" src="{{site.baseurl}}/images/HuskySpriteSheet.png">
        </canvas>
        <div id="controls"> <!--basic radio buttons which can be used to check whether each individual animaiton works -->
            <input type="radio" name="animation" id="idle" checked>
            <label for="idle">Idle</label><br>
            <input type="radio" name="animation" id="barking">
            <label for="barking">Barking</label><br>
            <input type="radio" name="animation" id="walking">
            <label for="walking">Walking</label><br>
            <input type="radio" name="animation" id="leaping" checked>
            <label for="leaping">Leaping</label><br>
            <input type="radio" name="animation" id="sitting">
            <label for="sitting">Sitting</label><br>
            <input type="radio" name="animation" id="sit command">
            <label for="sit command">Sit Command</label><br>
        </div>
    </div>
</body>
<script>
    // start on page load
    window.addEventListener('load', function () {
        const canvas = document.getElementById('spriteContainer');
        const ctx = canvas.getContext('2d');
        const SPRITE_WIDTH = 90;  // matches sprite pixel width
        const SPRITE_HEIGHT = 58; // matches sprite pixel height
        const SCALE_FACTOR = 2;  // control size of sprite on canvas
        const animationData = {
            'idle': {
                frameLimit: 4,
                x: 100, // X position for 'idle' animation
                y: 100, // Y position for 'idle' animation
            },
            'barking': {
                frameLimit: 4,
                x: 200, // X position for 'barking' animation
                y: 150, // Y position for 'barking' animation
            },
            'walking': {
                frameLimit: 6,
                x: 50, // X position for 'walking' animation
                y: 200, // Y position for 'walking' animation
            },
            'leaping': {
                frameLimit: 5,
                x: 50, // X position for 'walking' animation
                y: 200, // Y position for 'walking' animation
            },
            'sitting': {
                frameLimit: 4,
                x: 50, // X position for 'walking' animation
                y: 200, // Y position for 'walking' animation
            },
            'sit command': {
                frameLimit: 3,
                x: 50, // X position for 'walking' animation
                y: 200, // Y position for 'walking' animation
            }
        };
          // number of frames per row, this code assumes each row is different
        // const FRAME_RATE = 15;  // not used
        canvas.width = SPRITE_WIDTH * SCALE_FACTOR;
        canvas.height = SPRITE_HEIGHT * SCALE_FACTOR;
        class Husky {
            constructor() {
                this.image = document.getElementById("HuskySpriteSheet");
                this.spriteWidth = SPRITE_WIDTH;
                this.spriteHeight = SPRITE_HEIGHT;
                this.width = this.spriteWidth;
                this.height = this.spriteHeight;
                this.x = 0;
                this.y = 0;
                this.scale = SCALE_FACTOR;
                this.minFrame = 0;
            }
            setFrameLimit(limit) {
                this.maxFrame = limit;
            }
            setPosition(x, y) {
                this.x = x;
                this.y = y;
            }
            // draw husky object
            draw(context) {
                context.drawImage(
                    this.image,
                    this.frameX * this.spriteWidth,
                    this.frameY * this.spriteHeight,
                    this.spriteWidth,
                    this.spriteHeight,
                    this.x,
                    this.y,
                    this.width * this.scale,
                    this.height * this.scale
                );
            }
            // update frameX of object
            update() {
                if (this.frameX < this.maxFrame) {
                    this.frameX++;
                } else {
                    this.frameX = 0;
                }
            }
        }
        // husky object
        const husky = new Husky();
        // update frameY of husky object, action from idle, bark, walk, and other radio controls
        const controls = document.getElementById('controls');
        controls.addEventListener('click', function (event) {
            if (event.target.tagName === 'INPUT') {
                const selectedAnimation = event.target.id;
                const animationInfo = animationData[selectedAnimation];
                if (animationInfo) {
                    husky.setFrameLimit(animationInfo.frameLimit);
                    husky.setPosition(animationInfo.x, animationInfo.y);
                }
                switch (selectedAnimation) {
                    case 'idle':
                        husky.frameY = 5;
                        break;
                    case 'barking':
                        husky.frameY = 0;
                        break;
                    case 'walking':
                        husky.frameY = 1;
                        break;
                     case 'leaping':
                        husky.frameY = 2;
                        break;
                     case 'sitting':
                        husky.frameY = 3;
                        break;
                     case 'sit command':
                        husky.frameY = 4;
                        break;
                }
            }
        });
        // Animation recursive control function
        function animate() {
            // Clears the canvas to remove the previous frame.
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            // Draws the current frame of the sprite.
            husky.draw(ctx);
            // Updates the `frameX` property to prepare for the next frame in the sprite sheet.
            husky.update();
            // Uses `requestAnimationFrame` to synchronize the animation loop with the display's refresh rate,
            // ensuring smooth visuals.
            requestAnimationFrame(animate);
        }
        // run 1st animate
        animate();
    });
</script>