<html lang="da">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>Escape Auschwitz</title>

    <link rel="icon" type="image/png" href="favicon.png">

    <style>

        /* =====================================================
           SANS-SERIF SKRIFT PÅ HELE SIDEN
        ===================================================== */

        * {
            box-sizing: border-box;
            font-family: Arial, Helvetica, sans-serif;
        }

        body {
            margin: 0;
            font-family: Arial, Helvetica, sans-serif;
            background: #eee;
            color: #111;
            min-height: 100vh;
            overflow-x: hidden;
        }

        button {
            border: none;
            cursor: pointer;
            font-family: Arial, Helvetica, sans-serif;
        }


        /* =====================================================
           GENERELLE SKÆRME
        ===================================================== */

        .screen {
            min-height: 100vh;
            width: 100%;
            display: none;
            justify-content: center;
            align-items: center;
            padding: 30px;
        }

        .screen.active {
            display: flex;
        }


        /* =====================================================
           STARTSKÆRM
        ===================================================== */

        #startScreen {
            background: white;
            color: #111;
            text-align: center;
        }

        .start-content {
            display: flex;
            flex-direction: column;
            align-items: center;
            animation: startIn 1s ease;
        }

        @keyframes startIn {
            from {
                opacity: 0;
                transform: translateY(25px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .start-title {
            font-size: clamp(45px, 8vw, 95px);
            letter-spacing: 4px;
            margin: 0 0 15px 0;
            font-weight: bold;
            color: #111;
        }

        .start-subtitle {
            font-family: Arial, Helvetica, sans-serif;
            font-size: 18px;
            color: #666;
            margin-bottom: 45px;
        }

        .start-button {
            background: #111;
            color: white;
            padding: 18px 55px;
            border-radius: 40px;
            font-size: 22px;
            font-weight: bold;
            box-shadow: 0 8px 30px rgba(0,0,0,.15);
            transition: .25s;
        }

        .start-button:hover {
            background: #333;
            transform: translateY(-3px);
            box-shadow: 0 12px 35px rgba(0,0,0,.2);
        }

        .start-button:active {
            transform: scale(.97);
        }


        /* =====================================================
           REGELBOG
        ===================================================== */

        #rulesScreen {
            background:
                linear-gradient(
                    135deg,
                    #d7d1c4,
                    #eee9df
                );
            align-items: center;
        }

        .book {
            width: min(900px, 95vw);
            min-height: 650px;
            position: relative;

            background:
                linear-gradient(
                    90deg,
                    #d8c8a8 0%,
                    #f8f0dd 5%,
                    #f5ecd7 50%,
                    #e8dcc2 95%,
                    #cdbb98 100%
                );

            border-radius: 8px 18px 18px 8px;

            box-shadow:
                -15px 15px 0 #8f8066,
                -20px 20px 30px rgba(0,0,0,.35),
                inset 8px 0 15px rgba(0,0,0,.15);

            padding: 55px 70px 90px 80px;

            border-left: 8px solid #806f54;

            animation: bookOpen .7s cubic-bezier(.22,1,.36,1);
        }

        @keyframes bookOpen {
            from {
                opacity: 0;
                transform:
                    perspective(1200px)
                    rotateY(-18deg)
                    translateX(-30px);
            }

            to {
                opacity: 1;
                transform:
                    perspective(1200px)
                    rotateY(0)
                    translateX(0);
            }
        }

        .book::before {
            content: "";
            position: absolute;
            left: 58px;
            top: 0;
            bottom: 0;
            width: 2px;
            background: rgba(90,70,40,.25);
        }

        .book::after {
            content: "";
            position: absolute;
            top: 22px;
            bottom: 22px;
            right: 15px;
            width: 4px;
            border-radius: 5px;
            background: rgba(80,60,30,.18);
        }

        .book-title {
            text-align: center;
            font-size: 45px;
            margin: 0 0 8px 0;
            color: #2a241b;
        }

        .book-subtitle {
            text-align: center;
            font-family: Arial, Helvetica, sans-serif;
            color: #766b5a;
            margin-bottom: 35px;
        }

        .rule-section {
            margin-bottom: 28px;
        }

        .rule-section h2 {
            font-size: 26px;
            margin: 0 0 8px 0;
            color: #30281d;
        }

        .rule-section p {
            font-size: 18px;
            line-height: 1.65;
            margin: 0;
            color: #3c352b;
        }

        .rule-section ul {
            margin: 8px 0 0 0;
            padding-left: 25px;
        }

        .rule-section li {
            font-size: 18px;
            line-height: 1.65;
            margin-bottom: 5px;
        }

        .book-divider {
            height: 1px;
            background: rgba(70,50,25,.25);
            margin: 25px 0;
        }

        .book-footer {
            position: absolute;
            bottom: 22px;
            left: 80px;
            right: 55px;

            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 15px;
        }

        .book-page {
            font-size: 13px;
            color: #81745f;
        }

        .drawer-button {
            background: #211f1b;
            color: white;
            padding: 14px 25px;
            border-radius: 28px;
            font-size: 17px;
            font-weight: bold;
            transition: .25s;
        }

        .drawer-button:hover {
            transform: translateY(-2px);
            background: #000;
        }


        /* =====================================================
           TRÆKKER
        ===================================================== */

        #drawerScreen {
            background: white;
            align-items: center;
        }

        .game-container {
            width: 95%;
            max-width: 950px;
            padding: 28px;
            position: relative;
        }


        /* =====================================================
           TILBAGE TIL REGLER
        ===================================================== */

        .rules-back-button {
            position: fixed;
            top: 15px;
            right: 15px;
            z-index: 1100;

            background: #171717;
            color: white;

            /* GØR REGLER-KNAPPEN STØRRE */
            padding: 13px 22px;
            border-radius: 28px;

            font-size: 16px;
            font-weight: bold;

            box-shadow: 0 8px 30px rgba(0,0,0,.2);

            transition: .2s;
        }

        .rules-back-button:hover {
            transform: translateY(-2px);
            background: #333;
        }


        /* =====================================================
           MUSIKAFSPILLER
        ===================================================== */

        .music-player {
            position: fixed;
            top: 15px;
            left: 15px;

            width: 225px;

            background: #181818;
            color: white;

            border-radius: 12px;
            padding: 10px 11px;

            box-shadow:
                0 6px 20px rgba(0,0,0,.18);

            z-index: 2000;
        }

        .music-top {
            display: flex;
            align-items: center;
            gap: 9px;
        }

        .music-icon {
            width: 36px;
            height: 36px;
            flex-shrink: 0;

            border-radius: 6px;
            background: #303030;

            display: flex;
            align-items: center;
            justify-content: center;

            font-size: 20px;
        }

        .music-info {
            min-width: 0;
            flex: 1;
        }

        .music-title {
            font-size: 14px;
            font-weight: bold;

            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .music-status {
            font-size: 11px;
            color: #aaa;
            margin-top: 3px;
        }

        .music-controls {
            display: flex;
            justify-content: flex-end;
            gap: 6px;
            margin-top: 8px;
        }

        .music-control {
            width: 31px;
            height: 29px;

            padding: 0;
            border-radius: 50%;

            background: #303030;
            color: white;

            font-size: 13px;

            display: flex;
            align-items: center;
            justify-content: center;
        }

        .music-control:hover {
            background: #444;
        }

        .music-control:active {
            transform: scale(.94);
        }


        /* =====================================================
           MUSIK PÅ START OG REGLER
        ===================================================== */

        .start-music,
        .rules-music {
            position: fixed;
            top: 15px;
            left: 15px;
        }


        /* =====================================================
           KORT
        ===================================================== */

        .card {
            width: 100%;
            max-width: 360px;
            aspect-ratio: 6.3 / 8.8;

            background: #fafafa;

            border: 3px solid #111;
            border-radius: 12px;

            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;

            text-align: center;

            padding: 24px 18px;
            margin: 0 auto 24px auto;

            position: relative;
            overflow: hidden;

            perspective: 1000px;
        }

        .card.card-change {
            animation:
                cardSpin .7s
                cubic-bezier(.22,1,.36,1);
        }

        @keyframes cardSpin {
            0% {
                opacity: 0;
                transform:
                    rotateY(90deg)
                    scale(.85);
            }

            55% {
                opacity: 1;
                transform:
                    rotateY(-12deg)
                    scale(1.03);
            }

            100% {
                opacity: 1;
                transform:
                    rotateY(0deg)
                    scale(1);
            }
        }

        .small-title {
            color: #666;
            font-size: 15px;
            margin-bottom: 15px;
        }

        .question {
            width: 100%;

            font-size: 25px;
            font-weight: 600;
            line-height: 1.3;

            display: flex;
            align-items: center;
            justify-content: center;

            flex: 1;

            transition:
                transform .5s cubic-bezier(.22,1,.36,1),
                opacity .4s ease;
        }

        .answer {
            width: 100%;

            font-size: 20px;
            line-height: 1.35;

            color: #444;

            opacity: 0;
            transform: translateY(15px);

            max-height: 0;

            overflow: hidden;

            margin-top: 0;

            transition:
                opacity .45s ease,
                transform .45s ease,
                max-height .5s ease,
                margin-top .45s ease;
        }

        .answer.show {
            opacity: 1;
            transform: translateY(0);

            max-height: 180px;
            margin-top: 15px;
        }

        .card.answer-visible {
            justify-content: space-between;
        }

        .card.answer-visible .question {
            flex: 0 0 auto;
            transform: translateY(-5px);
        }


        /* =====================================================
           KNAPPER
        ===================================================== */

        .game-container button:not(.music-control):not(.rules-back-button) {
            border: none;
            cursor: pointer;

            font-size: 19px;
            font-weight: bold;

            border-radius: 30px;

            padding: 17px 25px;

            transition:
                transform .2s cubic-bezier(.22,1,.36,1),
                box-shadow .25s ease,
                background-color .25s ease;
        }

        .game-container button:hover:not(:disabled) {
            transform: translateY(-2px);
        }

        .game-container button:active:not(:disabled) {
            transform: translateY(1px) scale(.98);
        }

        .show-answer,
        .show-answer:disabled,
        .show-answer:hover:disabled,
        .next-button,
        .next-button:disabled,
        .next-button:hover:disabled {
            background: #171717 !important;
            color: white !important;
            opacity: 1 !important;
            filter: none !important;
            box-shadow: none !important;
        }

        .show-answer {
            width: 100%;
            margin-bottom: 15px;
        }

        .result-buttons {
            display: none;

            gap: 15px;
            margin-bottom: 15px;

            opacity: 0;
            transform: translateY(10px);
        }

        .result-buttons.show {
            display: flex;

            animation:
                resultButtonsIn .4s
                cubic-bezier(.22,1,.36,1)
                forwards;
        }

        @keyframes resultButtonsIn {
            from {
                opacity: 0;
                transform: translateY(12px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .correct {
            flex: 1;
            background: #dff5df;
            color: #207520;
        }

        .correct:hover:not(:disabled) {
            background: #ccefcf;
        }

        .wrong {
            flex: 1;
            background: #ffe1e1;
            color: #b32626;
        }

        .wrong:hover:not(:disabled) {
            background: #ffd0d0;
        }

        .next-button {
            width: 100%;
        }


        /* =====================================================
           EFFEKTER
        ===================================================== */

        .effect {
            display: none;

            padding: 20px;
            border-radius: 18px;

            margin-bottom: 20px;

            text-align: center;

            font-size: 20px;
            font-weight: bold;

            opacity: 0;
            transform: translateY(10px) scale(.98);
        }

        .effect.show {
            display: block;

            animation:
                effectIn .45s
                cubic-bezier(.22,1,.36,1)
                forwards;
        }

        @keyframes effectIn {
            0% {
                opacity: 0;
                transform:
                    translateY(12px)
                    scale(.97);
            }

            70% {
                transform:
                    translateY(-2px)
                    scale(1.01);
            }

            100% {
                opacity: 1;
                transform:
                    translateY(0)
                    scale(1);
            }
        }

        .good-effect {
            background: #e5f8e5;
            color: #217521;
        }

        .bad-effect {
            background: #ffe5e5;
            color: #b32626;
        }

        .restart {
            display: none;

            width: 100%;

            background: #3685e8;
            color: white;

            margin-top: 10px;

            animation:
                buttonIn .4s ease;
        }

        @keyframes buttonIn {
            from {
                opacity: 0;
                transform: translateY(8px);
            }

            to {
                opacity: 1;
                transform: translateY(0);
            }
        }


        /* =====================================================
           MOBIL
        ===================================================== */

        @media (max-width: 700px) {

            .book {
                padding:
                    40px
                    35px
                    95px
                    45px;

                min-height: 700px;
            }

            .book::before {
                left: 25px;
            }

            .book-title {
                font-size: 35px;
            }

            .rule-section h2 {
                font-size: 23px;
            }

            .rule-section p,
            .rule-section li {
                font-size: 16px;
            }

            .book-footer {
                left: 45px;
                right: 30px;

                flex-direction: column;
            }

            .drawer-button {
                width: 100%;
            }

            .game-container {
                padding: 18px;
            }

            .question {
                font-size: 23px;
            }

            .card {
                max-width: 300px;
            }

            .result-buttons {
                flex-direction: column;
            }

            .music-player {
                top: 10px;
                left: 10px;
                width: 200px;
            }

            .rules-back-button {
                top: 10px;
                right: 10px;
                padding: 12px 19px;
                font-size: 15px;
            }
        }

    </style>
</head>


<body>


    <!-- =====================================================
         STARTSKÆRM
    ===================================================== -->

    <section
        id="startScreen"
        class="screen active">

        <div class="music-player">

            <div class="music-top">

                <div class="music-icon">
                    ♫
                </div>

                <div class="music-info">

                    <div
                        class="music-title"
                        id="musicTitleStart">

                        Musik

                    </div>

                    <div
                        class="music-status"
                        id="musicStatusStart">

                        På pause

                    </div>

                </div>

            </div>

            <div class="music-controls">

                <button
                    class="music-control"
                    onclick="toggleMusic()">

                    ▶

                </button>

                <button
                    class="music-control"
                    onclick="nextMusic()">

                    ⏭

                </button>

            </div>

        </div>


        <div class="start-content">

            <h1 class="start-title">
                Escape Auschwitz
            </h1>

            <div class="start-subtitle">
                Et historisk spørgsmålsspil
            </div>

            <button
                class="start-button"
                onclick="showRules()">

                Regler

            </button>

        </div>

    </section>


    <!-- =====================================================
         REGELBOG
    ===================================================== -->

    <section
        id="rulesScreen"
        class="screen">

        <div class="music-player">

            <div class="music-top">

                <div class="music-icon">
                    ♫
                </div>

                <div class="music-info">

                    <div
                        class="music-title"
                        id="musicTitleRules">

                        Musik

                    </div>

                    <div
                        class="music-status"
                        id="musicStatusRules">

                        På pause

                    </div>

                </div>

            </div>

            <div class="music-controls">

                <button
                    class="music-control"
                    onclick="toggleMusic()">

                    ▶

                </button>

                <button
                    class="music-control"
                    onclick="nextMusic()">

                    ⏭

                </button>

            </div>

        </div>


        <div class="book">

            <h1 class="book-title">
                Regler
            </h1>

            <div class="book-subtitle">
                Escape Auschwitz
            </div>


            <div class="rule-section">

                <h2>
                    🎲 Sådan spiller I
                </h2>

                <p>
                    Spillerne bevæger sig rundt på spillepladen
                    ved hjælp af terningen. Følg reglerne på de
                    forskellige felter, når du lander på dem.
                </p>

            </div>


            <div class="book-divider"></div>


            <div class="rule-section">

                <h2>
                    ⛏️ Skovlen
                </h2>

                <p>
                    Lander du på en skovl, må du kaste med
                    terningen. Slår du en 4'er, 5'er eller 6'er,
                    må du grave en tunnel.
                </p>

                <p style="margin-top:10px;">
                    Tunnelen bliver liggende, så andre spillere
                    også kan bruge den.
                </p>

            </div>


            <div class="rule-section">

                <h2>
                    ❓ Spørgsmål
                </h2>

                <p>
                    Lander du på et spørgsmålstegn, skal du
                    trække et kort fra <strong>Trækkeren</strong>.
                </p>

                <ul>

                    <li>
                        Læs spørgsmålet.
                    </li>

                    <li>
                        Tryk på <strong>Vis svar</strong>.
                    </li>

                    <li>
                        Vælg <strong>Rigtigt</strong> eller
                        <strong>Forkert</strong>.
                    </li>

                    <li>
                        Et rigtigt svar giver en fordel.
                    </li>

                    <li>
                        Et forkert svar giver en straf.
                    </li>

                </ul>

            </div>


            <div class="rule-section">

                <h2>
                    ☠️ Hagekors-feltet
                </h2>

                <p>
                    Hvis du lander på et hagekors-felt,
                    bliver du sendt tilbage til start.
                </p>

            </div>


            <div class="rule-section">

                <h2>
                    🏁 Sådan vinder du
                </h2>

                <p>
                    Den spiller, der først lander på feltet
                    <strong>“Du er fri”</strong>, vinder spillet.
                </p>

            </div>


            <div class="book-footer">

                <span class="book-page">
                    Escape Auschwitz · Regelbog
                </span>

                <button
                    class="drawer-button"
                    onclick="showDrawer()">

                    Åbn trækkeren →

                </button>

            </div>

        </div>

    </section>


    <!-- =====================================================
         TRÆKKER
    ===================================================== -->

    <section
        id="drawerScreen"
        class="screen">

        <button
            class="rules-back-button"
            onclick="showRules()">

            📖 Regler

        </button>


        <div class="music-player">

            <div class="music-top">

                <div class="music-icon">
                    ♫
                </div>

                <div class="music-info">

                    <div
                        class="music-title"
                        id="musicTitle">

                        Musik

                    </div>

                    <div
                        class="music-status"
                        id="musicStatus">

                        På pause

                    </div>

                </div>

            </div>


            <div class="music-controls">

                <button
                    class="music-control"
                    id="playMusicButton"
                    onclick="toggleMusic()">

                    ▶

                </button>

                <button
                    class="music-control"
                    onclick="nextMusic()">

                    ⏭

                </button>

            </div>

        </div>


        <div class="game-container">

            <div
                class="card"
                id="card">

                <div class="small-title">
                    Spørgsmål
                </div>

                <div
                    class="question"
                    id="question">

                    Tryk på "Træk" for at få
                    et tilfældigt spørgsmål

                </div>

                <div
                    class="answer"
                    id="answer">
                </div>

            </div>


            <div
                class="effect"
                id="effect">
            </div>


            <button
                class="show-answer"
                id="showAnswer"
                onclick="showAnswer()"
                disabled>

                Vis svar

            </button>


            <div
                class="result-buttons"
                id="resultButtons">

                <button
                    class="correct"
                    id="correctButton"
                    onclick="correctAnswer()">

                    Rigtigt

                </button>

                <button
                    class="wrong"
                    id="wrongButton"
                    onclick="wrongAnswer()">

                    Forkert

                </button>

            </div>


            <button
                class="next-button"
                id="nextButton"
                onclick="drawCard()">

                Træk

            </button>


            <button
                class="restart"
                id="restartButton"
                onclick="restartGame()">

                Start forfra

            </button>

        </div>

    </section>



    <script>

        /* =====================================================
           SKÆRM-NAVIGATION
        ===================================================== */

        function hideAllScreens() {

            document
                .querySelectorAll(".screen")
                .forEach(screen => {

                    screen.classList.remove("active");

                });

        }


        function showStart() {

            hideAllScreens();

            document
                .getElementById("startScreen")
                .classList.add("active");

        }


        function showRules() {

            clearTimeout(answerTimer);
            answerTimer = null;

            hideAllScreens();

            document
                .getElementById("rulesScreen")
                .classList.add("active");

            updateMusicDisplay();

        }


        function showDrawer() {

            clearTimeout(answerTimer);
            answerTimer = null;

            hideAllScreens();

            document
                .getElementById("drawerScreen")
                .classList.add("active");

            updateMusicDisplay();

        }



        /* =====================================================
           LYDE
        ===================================================== */

        const correctSound =
            new Audio("Rigtig.mp3");

        const wrongSound =
            new Audio("Forkert.Mp3");

        const drawSound =
            new Audio("Træk.mp3");



        /* =====================================================
           BAGGRUNDSMUSIK
        ===================================================== */

        const backgroundMusic = [

            new Audio(
                "Brüder in Zechen.mp3"
            ),

            new Audio(
                "Erika.mp3"
            ),

            new Audio(
                "Die Braune Kompanie.mp3"
            )

        ];


        const musicNames = [

            "Brüder in Zechen",
            "Erika",
            "Die Braune Kompanie"

        ];


        let currentMusic = -1;
        let musicPlaying = false;


        function getRandomMusic() {

            let newMusic;

            do {

                newMusic =
                    Math.floor(
                        Math.random() *
                        backgroundMusic.length
                    );

            } while (

                backgroundMusic.length > 1 &&
                newMusic === currentMusic

            );

            return newMusic;

        }


        backgroundMusic.forEach(song => {

            song.volume = 0.01;

        });


        backgroundMusic.forEach(song => {

            song.addEventListener(
                "ended",
                () => {

                    if (!musicPlaying) {
                        return;
                    }

                    currentMusic =
                        getRandomMusic();

                    updateMusicDisplay();

                    playCurrentMusic();

                }
            );

        });


        function toggleMusic() {

            if (musicPlaying) {

                pauseBackgroundMusic();

            } else {

                startBackgroundMusic();

            }

        }


        function startBackgroundMusic() {

            if (currentMusic === -1) {

                currentMusic =
                    getRandomMusic();

            }

            musicPlaying = true;

            playCurrentMusic();

        }


        function pauseBackgroundMusic() {

            backgroundMusic.forEach(song => {

                song.pause();

            });

            musicPlaying = false;

            updateMusicDisplay();

        }


        function nextMusic() {

            backgroundMusic.forEach(song => {

                song.pause();

                song.currentTime = 0;

            });


            currentMusic =
                getRandomMusic();


            if (musicPlaying) {

                playCurrentMusic();

            } else {

                updateMusicDisplay();

            }

        }


        function playCurrentMusic() {

            if (!musicPlaying) {
                return;
            }


            const song =
                backgroundMusic[currentMusic];


            song.play()
                .then(() => {

                    updateMusicDisplay();

                })
                .catch(error => {

                    console.log(
                        "Musikken kunne ikke starte:",
                        error
                    );

                    musicPlaying = false;

                    updateMusicDisplay();

                });

        }


        /* =====================================================
           OPDATER MUSIKVISNING
        ===================================================== */

        function updateMusicDisplay() {

            const titleText =
                currentMusic >= 0
                    ? musicNames[currentMusic]
                    : "Musik";

            const statusText =
                musicPlaying
                    ? "Afspiller"
                    : "På pause";


            const title =
                document.getElementById("musicTitle");

            const status =
                document.getElementById("musicStatus");

            if (title) {
                title.textContent = titleText;
            }

            if (status) {
                status.textContent = statusText;
            }


            const startTitle =
                document.getElementById("musicTitleStart");

            const startStatus =
                document.getElementById("musicStatusStart");

            if (startTitle) {
                startTitle.textContent = titleText;
            }

            if (startStatus) {
                startStatus.textContent = statusText;
            }


            const rulesTitle =
                document.getElementById("musicTitleRules");

            const rulesStatus =
                document.getElementById("musicStatusRules");

            if (rulesTitle) {
                rulesTitle.textContent = titleText;
            }

            if (rulesStatus) {
                rulesStatus.textContent = statusText;
            }


            document
                .querySelectorAll(".music-control")
                .forEach(button => {

                    if (
                        button.textContent.trim() === "▶" ||
                        button.textContent.trim() === "Ⅱ"
                    ) {

                        button.textContent =
                            musicPlaying
                                ? "Ⅱ"
                                : "▶";

                    }

                });

        }


        /* =====================================================
           AUTOSTART MUSIK
        ===================================================== */

        function autoStartMusic() {

            if (musicPlaying) {
                return;
            }

            startBackgroundMusic();

        }


        window.addEventListener(
            "load",
            () => {

                autoStartMusic();

            }
        );


        document.addEventListener(
            "click",
            function startMusicAfterClick() {

                if (!musicPlaying) {

                    autoStartMusic();

                }

                document.removeEventListener(
                    "click",
                    startMusicAfterClick
                );

            },
            { once: true }
        );



        /* =====================================================
           LYD: RIGTIGT
        ===================================================== */

        function playCorrectSound() {

            correctSound.currentTime = 0;

            correctSound.play()
                .catch(error => {

                    console.log(
                        "Kunne ikke afspille Rigtig.mp3:",
                        error
                    );

                });

        }



        /* =====================================================
           LYD: FORKERT
        ===================================================== */

        function playWrongSound() {

            wrongSound.currentTime = 0;

            wrongSound.play()
                .catch(error => {

                    console.log(
                        "Kunne ikke afspille Forkert.Mp3:",
                        error
                    );

                });

        }



        /* =====================================================
           LYD: TRÆK
        ===================================================== */

        function playDrawSound() {

            drawSound.currentTime = 0;

            drawSound.play()
                .catch(error => {

                    console.log(
                        "Kunne ikke afspille Træk.mp3:",
                        error
                    );

                });

        }



        /* =====================================================
           SPØRGSMÅL
        ===================================================== */

        const cards = [

            {
                question: "Hvad var Auschwitz?",
                answer:
                    "Et stort nazistisk lejrkompleks."
            },

            {
                question:
                    "Hvornår blev Auschwitz oprettet?",
                answer:
                    "I 1940."
            },

            {
                question:
                    "Hvilke tre hoveddele bestod Auschwitz af?",
                answer:
                    "Auschwitz I, Auschwitz II-Birkenau og Auschwitz III-Monowitz."
            },

            {
                question:
                    "Hvad blev mange fanger sat til?",
                answer:
                    "Tvangsarbejde."
            },

            {
                question:
                    "Hvilken gruppe blev især forfulgt i Auschwitz?",
                answer:
                    "Europas jøder."
            },

            {
                question:
                    "Hvilke andre grupper blev sendt til Auschwitz?",
                answer:
                    "Blandt andre romaer, sintier, polakker og politiske modstandere."
            },

            {
                question:
                    "Blev børn sendt til Auschwitz?",
                answer:
                    "Ja."
            },

            {
                question:
                    "Hvordan var livet i lejren?",
                answer:
                    "Det var præget af sult, sygdom, hårdt arbejde og frygt."
            },

            {
                question:
                    "Hvor sov fangerne?",
                answer:
                    "Tæt sammen i barakker."
            },

            {
                question:
                    "Hvordan var hygiejnen i lejren?",
                answer:
                    "Den var meget dårlig."
            },

            {
                question:
                    "Hvad fik fangerne meget lidt af?",
                answer:
                    "Mad og rent vand."
            },

            {
                question:
                    "Hvem udførte menneskeforsøg?",
                answer:
                    "Nazistiske læger."
            },

            {
                question:
                    "Hvem lavede forsøg på tvillinger?",
                answer:
                    "Josef Mengele."
            },

            {
                question:
                    "Havde fangerne samtykket til forsøgene?",
                answer:
                    "Nej."
            },

            {
                question:
                    "Hvad kunne forsøgene føre til?",
                answer:
                    "Alvorlige skader eller død."
            },

            {
                question:
                    "Hvordan blev mange fanger dræbt?",
                answer:
                    "I gaskamre."
            },

            {
                question:
                    "Hvad kunne sult føre til?",
                answer:
                    "Svækkelse og død."
            },

            {
                question:
                    "Hvad skete der med mange fanger på grund af sygdom?",
                answer:
                    "De blev syge, og nogle døde."
            },

            {
                question:
                    "Hvad kunne tvangsarbejde føre til?",
                answer:
                    "Udmattelse og død."
            },

            {
                question:
                    "Hvad er Auschwitz i dag?",
                answer:
                    "Et mindested og museum."
            }

        ];



        /* =====================================================
           STRAFFE
        ===================================================== */

        const penalties = [

            "Vagterne kommer! – Gå 1 felt tilbage.",
            "Du bliver stoppet – Gå 2 felter tilbage.",
            "Du farer vild – Gå 3 felter tilbage.",
            "Porten er lukket – Spring din næste tur over.",
            "Du bliver sendt tilbage – Gå 3 felter tilbage.",
            "Alarm! – Gå 2 felter tilbage.",
            "Du mister tid – du bliver sprunget én tur over.",
            "Vejen er blokeret – Gå 1 felt tilbage.",
            "Du må gemme dig – Bliv stående i én omgang.",
            "Du bliver opdaget – Gå 2 felter tilbage."

        ];



        /* =====================================================
           FORDELE
        ===================================================== */

        const rewards = [

            "Vagterne går væk! – Gå 1 felt frem.",
            "Du finder en genvej – Gå 2 felter frem.",
            "Vejen er fri – Gå 2 felter frem.",
            "Du slipper forbi – Gå 3 felter frem.",
            "Du finder en skjult vej – Gå 3 felter frem.",
            "Vagterne kigger den anden vej – Gå 1 felt frem.",
            "Du får et forspring – Slå med terningen igen.",
            "Du når næsten ud – Gå 1 felt frem.",
            "Ingen opdager dig – Ryk 2 felter frem.",
            "Flugtvejen er åben! – Gå 3 felter frem."

        ];



        /* =====================================================
           SPILVARIABLER
        ===================================================== */

        let currentCard = null;
        let answerShown = false;
        let resultGiven = false;
        let answerTimer = null;



        /* =====================================================
           10 SEKUNDER
        ===================================================== */

        function startInactivityTimer() {

            clearTimeout(answerTimer);

            answerTimer = setTimeout(
                () => {

                    answerTimer = null;

                    restartGame();

                },
                10000
            );

        }



        /* =====================================================
           TRÆK KORT
        ===================================================== */

        function drawCard() {

            clearTimeout(answerTimer);

            answerTimer = null;

            playDrawSound();


            const cardElement =
                document.getElementById("card");

            const answer =
                document.getElementById("answer");

            const effect =
                document.getElementById("effect");

            const showButton =
                document.getElementById("showAnswer");

            const resultButtons =
                document.getElementById("resultButtons");

            const nextButton =
                document.getElementById("nextButton");


            answerShown = false;
            resultGiven = false;


            cardElement.classList.remove("answer-visible");

            answer.classList.remove("show");

            answer.textContent = "";
            answer.innerHTML = "";


            effect.classList.remove("show");

            effect.style.display = "none";

            effect.textContent = "";


            resultButtons.classList.remove("show");


            const randomIndex =
                Math.floor(
                    Math.random() * cards.length
                );


            currentCard =
                cards[randomIndex];


            document.getElementById("question").textContent =
                currentCard.question;


            cardElement.classList.remove("card-change");

            void cardElement.offsetWidth;

            cardElement.classList.add("card-change");


            showButton.disabled = false;

            showButton.style.display = "block";


            document.getElementById("correctButton").disabled = false;

            document.getElementById("wrongButton").disabled = false;


            nextButton.disabled = true;


            startInactivityTimer();

        }



        /* =====================================================
           VIS SVAR
        ===================================================== */

        function showAnswer() {

            if (!currentCard) {
                return;
            }

            if (answerShown) {
                return;
            }

            if (resultGiven) {
                return;
            }


            answerShown = true;


            const cardElement =
                document.getElementById("card");

            const answer =
                document.getElementById("answer");

            const showButton =
                document.getElementById("showAnswer");

            const resultButtons =
                document.getElementById("resultButtons");


            answer.textContent =
                currentCard.answer;


            cardElement.classList.add("answer-visible");


            answer.classList.remove("show");

            void answer.offsetWidth;

            answer.classList.add("show");


            showButton.disabled = true;


            resultButtons.classList.add("show");


            startInactivityTimer();

        }



        /* =====================================================
           RIGTIGT
        ===================================================== */

        function correctAnswer() {

            if (
                !answerShown ||
                resultGiven
            ) {
                return;
            }


            resultGiven = true;


            clearTimeout(answerTimer);

            answerTimer = null;


            playCorrectSound();


            const reward =
                rewards[
                    Math.floor(
                        Math.random() *
                        rewards.length
                    )
                ];


            const effect =
                document.getElementById("effect");


            effect.textContent =
                "Rigtigt! " + reward;


            effect.className =
                "effect good-effect";


            effect.style.display =
                "block";


            void effect.offsetWidth;


            effect.classList.add("show");


            finishResult();

        }



        /* =====================================================
           FORKERT
        ===================================================== */

        function wrongAnswer() {

            if (
                !answerShown ||
                resultGiven
            ) {
                return;
            }


            resultGiven = true;


            clearTimeout(answerTimer);

            answerTimer = null;


            playWrongSound();


            const penalty =
                penalties[
                    Math.floor(
                        Math.random() *
                        penalties.length
                    )
                ];


            const effect =
                document.getElementById("effect");


            effect.textContent =
                "Forkert! " + penalty;


            effect.className =
                "effect bad-effect";


            effect.style.display =
                "block";


            void effect.offsetWidth;


            effect.classList.add("show");


            finishResult();

        }



        /* =====================================================
           RESULTAT FÆRDIGT
        ===================================================== */

        function finishResult() {

            document
                .getElementById("resultButtons")
                .classList.remove("show");


            document
                .getElementById("nextButton")
                .disabled = false;


            startInactivityTimer();

        }



        /* =====================================================
           START FORFRA
        ===================================================== */

        function restartGame() {

            clearTimeout(answerTimer);

            answerTimer = null;


            currentCard = null;
            answerShown = false;
            resultGiven = false;


            const cardElement =
                document.getElementById("card");

            const answer =
                document.getElementById("answer");

            const effect =
                document.getElementById("effect");


            answer.classList.remove("show");

            answer.textContent = "";
            answer.innerHTML = "";


            cardElement.classList.remove("answer-visible");


            effect.classList.remove("show");

            effect.style.display = "none";

            effect.textContent = "";


            cardElement.classList.remove("card-change");

            void cardElement.offsetWidth;

            cardElement.classList.add("card-change");


            document.getElementById("question").textContent =
                'Tryk på "Træk" for at få et tilfældigt spørgsmål';


            document.getElementById("showAnswer").style.display =
                "block";

            document.getElementById("showAnswer").disabled =
                true;


            document
                .getElementById("resultButtons")
                .classList.remove("show");


            document.getElementById("nextButton").style.display =
                "block";

            document.getElementById("nextButton").disabled =
                false;

            document.getElementById("nextButton").textContent =
                "Træk";


            document.getElementById("restartButton").style.display =
                "none";


            document.getElementById("correctButton").disabled =
                false;

            document.getElementById("wrongButton").disabled =
                false;

        }

    </script>

</body>

</html>
