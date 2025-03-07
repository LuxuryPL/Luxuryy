<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kiedy spadną metiny</title>
    <meta name="author" content="LuxuryPL">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: url('https://source.unsplash.com/1600x900/?tango,dance') no-repeat center center fixed;
            background-size: cover;
            color: white;
            padding: 50px;
        }
        h1 {
            font-size: 36px;
            background-color: rgba(0, 0, 0, 0.6);
            display: inline-block;
            padding: 10px 20px;
            border-radius: 10px;
        }
        #countdown, #lastResp, #nextResps {
            font-family: 'Orbitron', sans-serif;
            font-size: 28px;
            font-weight: bold;
            margin-top: 10px;
            background-color: rgba(0, 0, 0, 0.6);
            display: inline-block;
            padding: 10px;
            border-radius: 10px;
        }
        #countdown {
            color: #ffcc00;
        }
        #lastResp {
            color: #ff4444;
        }
        .resp-list {
            margin-top: 20px;
        }
        .maps {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
        }
        .map-button {
            background-color: #6b2f2f;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 18px;
        }
        .map-button:hover {
            background-color: #8c3b3b;
        }
    </style>
</head>
<body>

    <h1>Kiedy spadną metiny?</h1>
    <p>Najbliższy resp: <span id="countdown"></span></p>
    <p>Ostatni resp: <span id="lastResp"></span></p>
    
    <button onclick="showNextResps()">Kolejne 12 respów</button>
    <div id="nextResps" class="resp-list"></div>

    <h2>🗺️ Mapy Shinsoo 🗺️</h2>
    <div class="maps">
        <button class="map-button">Shinsoo M1</button>
        <button class="map-button">Shinsoo M2</button>
        <button class="map-button">Pustynia Yongbi</button>
        <button class="map-button">Ognista Ziemia</button>
        <button class="map-button">Zielony Las</button>
        <button class="map-button">Czerwony Las</button>
    </div>

    <script>
        const respawnInterval = 1 * 60 * 60 * 1000 + 1 * 60 * 1000; // 1 godzina 1 minuta

        function getNextRespawnTime() {
            const now = new Date();
            const referenceTime = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 0, 0, 0);
            let nextRespawn = referenceTime.getTime();

            while (nextRespawn <= now.getTime()) {
                nextRespawn += respawnInterval;
            }

            return nextRespawn;
        }

        function updateCountdown() {
            const nextRespawn = getNextRespawnTime();
            const now = new Date().getTime();
            const timeLeft = nextRespawn - now;
            const lastRespawn = nextRespawn - respawnInterval;

            if (timeLeft <= 0) {
                document.getElementById("countdown").innerHTML = "Metiny już spadły!";
            } else {
                const minutes = Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60));
                const seconds = Math.floor((timeLeft % (1000 * 60)) / 1000);

                document.getElementById("countdown").innerHTML = `${minutes} minut, ${seconds} sekund`;
            }

            const lastMinutes = Math.floor(((now - lastRespawn) % (1000 * 60 * 60)) / (1000 * 60));
            const lastSeconds = Math.floor(((now - lastRespawn) % (1000 * 60)) / 1000);

            document.getElementById("lastResp").innerHTML = `${lastMinutes} minut, ${lastSeconds} sekund temu`;
        }

        function showNextResps() {
            let output = "<h2>Następne 12 respawnów</h2>";
            let nextTime = getNextRespawnTime();
            
            for (let i = 0; i < 12; i++) {
                let date = new Date(nextTime);
                output += `<p>${date.getHours()}:${String(date.getMinutes()).padStart(2, "0")}</p>`;
                nextTime += respawnInterval;
            }

            document.getElementById("nextResps").innerHTML = output;
        }

        setInterval(updateCountdown, 1000);
        updateCountdown();
    </script>

</body>
</html># Luxuryy
