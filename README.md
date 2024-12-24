<section class="section" id="decorate-tree">
    <h2>Decorate the Christmas Tree</h2>
    <div id="tree-container" style="position: relative; margin: auto; width: 300px; height: 400px;">
        <img src="https://via.placeholder.com/300x400?text=Tree" id="tree" style="width: 100%; height: auto;">
    </div>
    <div id="ornaments">
        <img src="https://via.placeholder.com/50x50?text=Ball1" draggable="true" class="ornament">
        <img src="https://via.placeholder.com/50x50?text=Ball2" draggable="true" class="ornament">
        <img src="https://via.placeholder.com/50x50?text=Ball3" draggable="true" class="ornament">
    </div>
</section>

<script>
    const ornaments = document.querySelectorAll('.ornament');
    const treeContainer = document.getElementById('tree-container');

    ornaments.forEach(ornament => {
        ornament.addEventListener('dragstart', (e) => {
            e.dataTransfer.setData('text/plain', e.target.id);
        });
    });

    treeContainer.addEventListener('dragover', (e) => {
        e.preventDefault();
    });

    treeContainer.addEventListener('drop', (e) => {
        e.preventDefault();
        const id = e.dataTransfer.getData('text');
        const ornament = document.getElementById(id);
        ornament.style.position = 'absolute';
        ornament.style.left = e.offsetX + 'px';
        ornament.style.top = e.offsetY + 'px';
        treeContainer.appendChild(ornament);
    });
</script>
<section class="section" id="gift-boxes">
    <h2>Open a Gift!</h2>
    <div class="gift-box" onclick="revealMessage('gift1')">
        🎁 Click Me!
    </div>
    <div id="gift1" style="display: none;">
        🎉 Surprise! Wishing you a joyful Christmas! 🎄
    </div>
</section>

<script>
    function revealMessage(id) {
        const message = document.getElementById(id);
        message.style.display = message.style.display === 'none' ? 'block' : 'none';
    }
</script>
<section class="section" id="snowball-game">
    <h2>Throw a Snowball!</h2>
    <div id="snowball" onclick="throwSnowball()" style="width: 50px; height: 50px; background: white; border-radius: 50%; position: relative; margin: auto;">
        ❄️
    </div>
</section>

<script>
    function throwSnowball() {
        const snowball = document.getElementById('snowball');
        snowball.style.animation = 'throw 2s linear';
        setTimeout(() => snowball.style.animation = '', 2000);
    }

    document.styleSheets[0].insertRule(`
        @keyframes throw {
            0% { transform: translateY(0); }
            100% { transform: translateY(-300px) translateX(200px); opacity: 0; }
        }
    `, 0);
</script>
<section class="section" id="ecard">
    <h2>Create Your Christmas Card</h2>
    <form id="ecard-form">
        <label for="name">Your Name:</label>
        <input type="text" id="name" required>
        <label for="message">Your Message:</label>
        <textarea id="message" required></textarea>
        <button type="button" onclick="generateCard()">Generate Card</button>
    </form>
    <canvas id="ecard-canvas" style="display: none; border: 1px solid #fff; margin-top: 20px;"></canvas>
</section>

<script>
    function generateCard() {
        const name = document.getElementById('name').value;
        const message = document.getElementById('message').value;
        const canvas = document.getElementById('ecard-canvas');
        const ctx = canvas.getContext('2d');
        canvas.style.display = 'block';
        canvas.width = 400;
        canvas.height = 300;

        // Background
        ctx.fillStyle = '#ff6b6b';
        ctx.fillRect(0, 0, canvas.width, canvas.height);

        // Text
        ctx.fillStyle = '#fff';
        ctx.font = '20px Arial';
        ctx.fillText('Merry Christmas!', 100, 50);
        ctx.fillText(`From: ${name}`, 100, 100);
        ctx.fillText(message, 100, 150);

        // Download option
        const link = document.createElement('a');
        link.download = 'Christmas_Card.png';
        link.href = canvas.toDataURL();
        link.textContent = 'Download Card';
        document.getElementById('ecard').appendChild(link);
    }
</script>
