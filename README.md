# Rsv-codage
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RSV </title>
    <style>
        :root {
            --mec-color: rgba(0, 123, 255, 0.7);
            --meuf-color: rgba(255, 0, 127, 0.7);
            --travail-color: rgba(255, 165, 0, 0.7);
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 0;
            color: white;
            min-height: 100vh;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        .main-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        @media (max-width: 900px) {
            .main-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .panel {
            background-color: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
        }
        
        h1 {
            text-align: center;
            margin-bottom: 30px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            grid-column: 1 / -1;
        }
        
        .section {
            display: none;
        }
        
        .active {
            display: block;
        }
        
        .salon-buttons {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }
        
        .salon-btn {
            flex: 1;
            min-width: 120px;
            padding: 12px;
            background-color: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 25px;
            color: white;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .salon-btn:hover {
            background-color: rgba(255, 255, 255, 0.3);
        }
        
        .salon-btn.active {
            font-weight: bold;
        }
        
        #mecsBtn.active { background-color: var(--mec-color); }
        #meufsBtn.active { background-color: var(--meuf-color); }
        #travailBtn.active { background-color: var(--travail-color); }
        
        #mecsBtn { background-color: var(--mec-color); }
        #meufsBtn { background-color: var(--meuf-color); }
        #travailBtn { background-color: var(--travail-color); }
        
        input, button, select, textarea {
            padding: 12px;
            margin: 8px 0;
            border: none;
            border-radius: 25px;
            width: 100%;
            font-size: 16px;
        }
        
        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: #45a049;
        }
        
        .chat-container {
            display: flex;
            flex-direction: column;
            height: 300px;
        }
        
        #messages {
            flex: 1;
            overflow-y: auto;
            background-color: rgba(255, 255, 255, 0.2);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
        }
        
        .message {
            margin-bottom: 10px;
            padding: 8px 12px;
            background-color: rgba(255, 255, 255, 0.3);
            border-radius: 18px;
            display: inline-block;
            max-width: 70%;
            word-break: break-word;
        }
        
        .user-count {
            text-align: right;
            font-style: italic;
            margin-bottom: 10px;
        }
        
        .notification {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: rgba(0, 0, 0, 0.7);
            color: white;
            padding: 15px;
            border-radius: 10px;
            display: none;
            z-index: 1000;
        }
        
        /* Éditeur de code */
        .editor-container {
            display: flex;
            flex-direction: column;
            height: 300px;
        }
        
        .editor-toolbar {
            display: flex;
            gap: 10px;
            margin-bottom: 10px;
        }
        
        .editor-toolbar button {
            flex: 1;
        }
        
        #codeEditor {
            flex: 1;
            background-color: #1e1e1e;
            color: #d4d4d4;
            font-family: 'Consolas', monospace;
            padding: 10px;
            border-radius: 5px;
            resize: none;
            white-space: pre;
        }
        
        #codeOutput {
            flex: 1;
            background-color: white;
            color: black;
            padding: 10px;
            border-radius: 5px;
            overflow: auto;
        }
        
        .tab-buttons {
            display: flex;
            margin-bottom: 10px;
        }
        
        .tab-btn {
            padding: 10px;
            background-color: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            cursor: pointer;
        }
        
        .tab-btn.active {
            background-color: rgba(255, 255, 255, 0.4);
            font-weight: bold;
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Espace Codage entre Amis</h1>
        
        <div id="loginSection" class="section active">
            <h2>Connectez-vous</h2>
            <input type="text" id="username" placeholder="Votre pseudo" required>
            <select id="gender">
                <option value="mec">Je suis un mec</option>
                <option value="meuf">Je suis une meuf</option>
            </select>
            <button id="loginBtn">Entrer dans l'espace</button>
        </div>
        
        <div id="mainSection" class="section">
            <div class="main-grid">
                <div class="panel">
                    <div class="salon-buttons">
                        <button id="mecsBtn" class="salon-btn">Entre Mecs</button>
                        <button id="meufsBtn" class="salon-btn">Entre Meufs</button>
                        <button id="travailBtn" class="salon-btn active">Travaux/Exercices</button>
                    </div>
                    
                    <div class="user-count">En ligne: <span id="userCount">0</span></div>
                    
                    <div class="chat-container">
                        <div id="messages"></div>
                        <input type="text" id="messageInput" placeholder="Écrivez votre message...">
                        <button id="sendBtn">Envoyer</button>
                    </div>
                </div>
                
                <div class="panel">
                    <div class="tab-buttons">
                        <button class="tab-btn active" onclick="openTab('htmlTab')">HTML</button>
                        <button class="tab-btn" onclick="openTab('cssTab')">CSS</button>
                        <button class="tab-btn" onclick="openTab('jsTab')">JavaScript</button>
                        <button class="tab-btn" onclick="openTab('outputTab')">Résultat</button>
                    </div>
                    
                    <div id="htmlTab" class="tab-content active">
                        <div class="editor-container">
                            <textarea id="htmlEditor" class="code-editor" placeholder="Écrivez votre code HTML ici...">&lt;!DOCTYPE html&gt;
&lt;html&gt;
&lt;head&gt;
    &lt;title&gt;Mon Programme&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;Bonjour le monde !&lt;/h1&gt;
    &lt;p id="demo"&gt;Ceci est un exemple.&lt;/p&gt;
    &lt;button onclick="changeText()"&gt;Cliquez-moi&lt;/button&gt;
&lt;/body&gt;
&lt;/html&gt;</textarea>
                        </div>
                    </div>
                    
                    <div id="cssTab" class="tab-content">
                        <div class="editor-container">
                            <textarea id="cssEditor" class="code-editor" placeholder="Écrivez votre code CSS ici...">body {
    font-family: Arial, sans-serif;
    text-align: center;
    padding: 20px;
}

h1 {
    color: #4CAF50;
}</textarea>
                        </div>
                    </div>
                    
                    <div id="jsTab" class="tab-content">
                        <div class="editor-container">
                            <textarea id="jsEditor" class="code-editor" placeholder="Écrivez votre code JavaScript ici...">function changeText() {
    document.getElementById("demo").innerHTML = "Vous avez cliqué !";
    alert("Fonction exécutée !");
}</textarea>
                        </div>
                    </div>
                    
                    <div id="outputTab" class="tab-content">
                        <div class="editor-container">
                            <iframe id="codeOutput" frameborder="0"></iframe>
                        </div>
                    </div>
                    
                    <div class="editor-toolbar">
                        <button id="runBtn">Exécuter</button>
                        <button id="shareBtn">Partager</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <div class="notification" id="notification">
        Nouveau message dans <span id="salonNotif"></span> !
    </div>
    
    <audio id="notificationSound" preload="auto">
        <source src="https://assets.mixkit.co/sfx/preview/mixkit-software-interface-start-2574.mp3" type="audio/mpeg">
    </audio>

    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>
    
    <script>
        // Configuration Firebase (à remplacer par votre config)
        const firebaseConfig = {
            apiKey: "AIzaSyDEXAMPLEEXAMPLEEXAMPLE",
            authDomain: "votre-projet.firebaseapp.com",
            databaseURL: "https://votre-projet-default-rtdb.firebaseio.com",
            projectId: "votre-projet",
            storageBucket: "votre-projet.appspot.com",
            messagingSenderId: "1234567890",
            appId: "1:1234567890:web:abc123def456"
        };
        
        // Initialisation Firebase
        firebase.initializeApp(firebaseConfig);
        const database = firebase.database();
        
        // Références
        let currentSalon = "travail";
        let currentUser = null;
        let userGender = null;
        let userRef = null;
        let codeRef = null;
        
        // Éléments DOM
        const loginSection = document.getElementById('loginSection');
        const mainSection = document.getElementById('mainSection');
        const usernameInput = document.getElementById('username');
        const genderSelect = document.getElementById('gender');
        const loginBtn = document.getElementById('loginBtn');
        const mecsBtn = document.getElementById('mecsBtn');
        const meufsBtn = document.getElementById('meufsBtn');
        const travailBtn = document.getElementById('travailBtn');
        const messageInput = document.getElementById('messageInput');
        const sendBtn = document.getElementById('sendBtn');
        const messagesDiv = document.getElementById('messages');
        const userCountSpan = document.getElementById('userCount');
        const notification = document.getElementById('notification');
        const salonNotif = document.getElementById('salonNotif');
        const notificationSound = document.getElementById('notificationSound');
        
        // Éditeur de code
        const htmlEditor = document.getElementById('htmlEditor');
        const cssEditor = document.getElementById('cssEditor');
        const jsEditor = document.getElementById('jsEditor');
        const codeOutput = document.getElementById('codeOutput');
        const runBtn = document.getElementById('runBtn');
        const shareBtn = document.getElementById('shareBtn');
        
        // Gestion des onglets
        function openTab(tabId) {
            const tabContents = document.getElementsByClassName('tab-content');
            for (let i = 0; i < tabContents.length; i++) {
                tabContents[i].classList.remove('active');
            }
            
            const tabButtons = document.getElementsByClassName('tab-btn');
            for (let i = 0; i < tabButtons.length; i++) {
                tabButtons[i].classList.remove('active');
            }
            
            document.getElementById(tabId).classList.add('active');
            event.currentTarget.classList.add('active');
        }
        
        // Exécuter le code
        function runCode() {
            const html = htmlEditor.value;
            const css = `<style>${cssEditor.value}</style>`;
            const js = `<script>${jsEditor.value}<\/script>`;
            
            const outputDoc = codeOutput.contentDocument || codeOutput.contentWindow.document;
            outputDoc.open();
            outputDoc.write(html + css + js);
            outputDoc.close();
            
            // Sauvegarder le code dans Firebase
            if (codeRef) {
                codeRef.set({
                    html: html,
                    css: cssEditor.value,
                    js: jsEditor.value,
                    timestamp: firebase.database.ServerValue.TIMESTAMP,
                    user: currentUser
                });
            }
        }
        
        // Partager le code
        function shareCode() {
            if (currentSalon === "mecs" && userGender !== "mec") {
                alert("Accès réservé aux mecs dans ce salon !");
                return;
            }
            
            if (currentSalon === "meufs" && userGender !== "meuf") {
                alert("Accès réservé aux meufs dans ce salon !");
                return;
            }
            
            const codeData = {
                html: htmlEditor.value,
                css: cssEditor.value,
                js: jsEditor.value,
                user: currentUser,
                salon: currentSalon,
                timestamp: firebase.database.ServerValue.TIMESTAMP
            };
            
            database.ref('sharedCode').push().set(codeData);
            alert("Code partagé dans le salon !");
        }
        
        // Gestion des salons
        function changeSalon(salon) {
            currentSalon = salon;
            
            // Mettre à jour les boutons actifs
            mecsBtn.classList.remove('active');
            meufsBtn.classList.remove('active');
            travailBtn.classList.remove('active');
            
            if (salon === "mecs") mecsBtn.classList.add('active');
            if (salon === "meufs") meufsBtn.classList.add('active');
            if (salon === "travail") travailBtn.classList.add('active');
            
            // Vérifier les accès
            if ((salon === "mecs" && userGender !== "mec") || 
                (salon === "meufs" && userGender !== "meuf")) {
                messagesDiv.innerHTML = "<div class='message'>🚫 Accès réservé</div>";
                messageInput.disabled = true;
            } else {
                messageInput.disabled = false;
                loadMessages();
                loadSharedCode();
            }
        }
        
        // Charger les messages
        function loadMessages() {
            messagesDiv.innerHTML = "";
            database.ref('messages/' + currentSalon).limitToLast(50).on('child_added', (snapshot) => {
                const message = snapshot.val();
                displayMessage(message);
            });
        }
        
        // Charger le code partagé
        function loadSharedCode() {
            database.ref('sharedCode').orderByChild('salon').equalTo(currentSalon).limitToLast(1).on('child_added', (snapshot) => {
                const code = snapshot.val();
                if (code.user !== currentUser) {
                    htmlEditor.value = code.html || "";
                    cssEditor.value = code.css || "";
                    jsEditor.value = code.js || "";
                    runCode();
                    
                    // Notification
                    salonNotif.textContent = currentSalon === "mecs" ? "Entre Mecs" : 
                                           currentSalon === "meufs" ? "Entre Meufs" : "Travaux/Exercices";
                    notificationSound.play();
                    notification.style.display = 'block';
                    setTimeout(() => {
                        notification.style.display = 'none';
                    }, 3000);
                }
            });
        }
        
        // Connexion
        loginBtn.addEventListener('click', () => {
            const username = usernameInput.value.trim();
            userGender = genderSelect.value;
            
            if (username) {
                currentUser = username;
                
                // Enregistrer l'utilisateur
                userRef = database.ref('users').push();
                userRef.set({
                    name: username,
                    gender: userGender,
                    timestamp: firebase.database.ServerValue.TIMESTAMP
                });
                
                // Référence pour le code partagé
                codeRef = database.ref('userCode/' + currentUser.replace(/\./g, '_'));
                
                // Mettre à jour le compteur
                database.ref('users').on('value', (snapshot) => {
                    const users = snapshot.val();
                    const count = users ? Object.keys(users).length : 0;
                    userCountSpan.textContent = count;
                });
                
                // Afficher le chat
                loginSection.classList.remove('active');
                mainSection.classList.add('active');
                changeSalon("travail");
                messageInput.focus();
                
                // Écouter les nouveaux messages pour notifications
                setupNotifications();
                
                // Charger le dernier code sauvegardé
                codeRef.on('value', (snapshot) => {
                    const code = snapshot.val();
                    if (code) {
                        htmlEditor.value = code.html || "";
                        cssEditor.value = code.css || "";
                        jsEditor.value = code.js || "";
                        runCode();
                    }
                });
            }
        });
        
        // Boutons salons
        mecsBtn.addEventListener('click', () => changeSalon("mecs"));
        meufsBtn.addEventListener('click', () => changeSalon("meufs"));
        travailBtn.addEventListener('click', () => changeSalon("travail"));
        
        // Envoyer message
        sendBtn.addEventListener('click', sendMessage);
        messageInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });
        
        function sendMessage() {
            const messageText = messageInput.value.trim();
            if (messageText && currentUser && 
                !((currentSalon === "mecs" && userGender !== "mec") || 
                  (currentSalon === "meufs" && userGender !== "meuf"))) {
                
                databas