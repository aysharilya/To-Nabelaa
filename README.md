<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Happy Birthday Nabela</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Quicksand:wght@400;600&display=swap');

        body {
            font-family: 'Quicksand', sans-serif;
            background-color: #ffe4e1;
            margin: 0;
            overflow: hidden;
            color: #d81b60;
        }

        .pink-theme {
            background: linear-gradient(135deg, #ffc0cb 0%, #ff69b4 100%);
        }

        .font-birthday {
            font-family: 'Dancing Script', cursive;
        }

        /* Animasi Lilin */
        .flame {
            width: 15px;
            height: 25px;
            background: #ffdb58;
            border-radius: 50% 50% 35% 35%;
            position: absolute;
            top: -25px;
            left: 50%;
            transform: translateX(-50%);
            animation: flicker 0.1s ease-in infinite;
            box-shadow: 0 0 10px #ffdb58, 0 0 20px #ffdb58;
        }

        @keyframes flicker {
            0% { transform: translateX(-50%) scale(1); }
            50% { transform: translateX(-50%) scale(1.1) rotate(2deg); }
            100% { transform: translateX(-50%) scale(1) rotate(-2deg); }
        }

        /* Ornamen Ulang Tahun */
        .balloon {
            position: absolute;
            width: 50px;
            height: 70px;
            background: #ff69b4;
            border-radius: 50%;
            bottom: -100px;
            animation: float 6s ease-in infinite;
            opacity: 0.7;
        }

        @keyframes float {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-120vh) rotate(20deg); opacity: 0; }
        }

        .floating-text {
            animation: bounce 2s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .cake-container {
            cursor: pointer;
            transition: transform 0.3s;
        }

        .cake-container:hover {
            transform: scale(1.05);
        }

        .hidden {
            display: none;
        }

        /* Confetti Effect */
        .confetti {
            position: absolute;
            width: 10px;
            height: 10px;
            background-color: #f2d74e;
            animation: confetti-fall 3s linear infinite;
        }

        @keyframes confetti-fall {
            0% { transform: translateY(-10vh) rotate(0deg); }
            100% { transform: translateY(110vh) rotate(360deg); }
        }
    </style>
</head>
<body class="h-screen flex items-center justify-center relative">

    <!-- Background Ornaments -->
    <div id="ornaments"></div>

    <!-- Halaman 1: Tiup Lilin -->
    <div id="page1" class="text-center z-10 flex flex-col items-center">
        <h1 class="text-5xl md:text-6xl font-birthday mb-8 floating-text drop-shadow-lg">Happy Birthday Nabela</h1>
        
        <div class="cake-container relative mt-10" onclick="blowCandle()">
            <!-- Cake Body (CSS Shape) -->
            <div class="w-48 h-32 bg-pink-300 rounded-t-lg relative border-b-8 border-pink-400 shadow-xl">
                <!-- Cream drips -->
                <div class="absolute -bottom-2 flex w-full justify-around">
                    <div class="w-8 h-8 bg-pink-300 rounded-full"></div>
                    <div class="w-8 h-8 bg-pink-300 rounded-full"></div>
                    <div class="w-8 h-8 bg-pink-300 rounded-full"></div>
                    <div class="w-8 h-8 bg-pink-300 rounded-full"></div>
                    <div class="w-8 h-8 bg-pink-300 rounded-full"></div>
                </div>
                
                <!-- Candle -->
                <div id="candle" class="w-3 h-12 bg-white absolute -top-12 left-1/2 -translate-x-1/2 rounded-full border-2 border-pink-100">
                    <div id="flame" class="flame"></div>
                </div>
            </div>
            <!-- Cake Base -->
            <div class="w-56 h-4 bg-white rounded-full mt-2 shadow-md"></div>
        </div>

        <p class="mt-12 text-xl font-semibold animate-pulse italic">"Klik lilin untuk meniupnya"</p>
        
        <!-- Hint for Audio -->
        <p class="text-xs mt-4 text-pink-700 opacity-50">(Pastikan volume menyala untuk lagu)</p>
    </div>

    <!-- Halaman 2: Doa -->
    <div id="page2" class="hidden text-center z-10 px-6 max-w-2xl">
        <div class="bg-white/80 backdrop-blur-sm p-10 rounded-3xl shadow-2xl border-4 border-pink-200">
            <h2 class="text-4xl font-birthday mb-6">Barakallah Fii Umrik!</h2>
            <div class="space-y-4 text-lg leading-relaxed text-pink-800">
                <p>Semoga panjang umur, sehat selalu, dan apa yang diimpikan segera tercapai.</p>
                <p class="font-bold text-2xl py-4">"Semoga apa yang disemogakan tersemogakan"</p>
                <p>Hari ini adalah harimu, Nabela. Teruslah bersinar dan bahagia!</p>
            </div>
            <button onclick="location.reload()" class="mt-8 bg-pink-500 text-white px-6 py-2 rounded-full hover:bg-pink-600 transition shadow-lg">
                Lihat Lagi ✨
            </button>
        </div>
    </div>

    <!-- Audio Player (Hidden) -->
    <audio id="bgMusic" loop>
        <source src="https://youtu.be/IzvZ0gOXiNA?si=YarVMbRDrCbIfoTu" type="audio/mpeg">
        <!-- Catatan: Menggunakan placeholder audio. Untuk hasil terbaik, ganti dengan URL mp3 lagu Happy Birthday -->
    </audio>

    <script>
        // Inisialisasi Ornamen
        const ornamentsContainer = document.getElementById('ornaments');
        const colors = ['#ffb6c1', '#ff69b4', '#ffc0cb', '#da70d6', '#ffffff'];

        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.className = 'balloon';
            balloon.style.left = Math.random() * 100 + 'vw';
            balloon.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            balloon.style.animationDuration = (Math.random() * 3 + 4) + 's';
            ornamentsContainer.appendChild(balloon);
            setTimeout(() => balloon.remove(), 7000);
        }

        function createConfetti() {
            const confetti = document.createElement('div');
            confetti.className = 'confetti';
            confetti.style.left = Math.random() * 100 + 'vw';
            confetti.style.backgroundColor = colors[Math.floor(Math.random() * colors.length)];
            confetti.style.width = Math.random() * 10 + 5 + 'px';
            confetti.style.height = confetti.style.width;
            confetti.style.animationDuration = (Math.random() * 2 + 2) + 's';
            ornamentsContainer.appendChild(confetti);
            setTimeout(() => confetti.remove(), 4000);
        }

        // Mulai ornamen
        setInterval(createBalloon, 1500);

        // Fungsi Tiup Lilin
        function blowCandle() {
            const flame = document.getElementById('flame');
            const page1 = document.getElementById('page1');
            const page2 = document.getElementById('page2');
            const music = document.getElementById('bgMusic');

            // Play music (browser butuh interaksi user)
            music.play().catch(e => console.log("Audio play failed, waiting for more interaction"));

            // Matikan lilin
            flame.style.display = 'none';

            // Efek transisi
            setTimeout(() => {
                page1.classList.add('hidden');
                page2.classList.remove('hidden');
                
                // Tambah selebrasi confetti
                setInterval(createConfetti, 100);
            }, 800);
        }

        // Auto-play music attempt on first click anywhere
        document.body.addEventListener('click', () => {
            const music = document.getElementById('bgMusic');
            if (music.paused) music.play();
        }, { once: true });
    </script>
</body>
</html>
