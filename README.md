<!DOCTYPE html>
<html lang="ro">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BNR MFA - Autentificare Securizată</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body { background-color: #002147; }
        .bnr-card { border-top: 5px solid #c5a059; }
    </style>
</head>
<body class="flex items-center justify-center min-h-screen font-sans">

    <!-- 1. LOGIN SECTION -->
    <div id="loginCard" class="bg-white p-10 bnr-card rounded shadow-2xl w-[400px] text-center">
        <div class="mb-8">
            <h1 class="text-3xl font-serif font-bold text-[#002147] tracking-tight">
                BANCA NAȚIONALĂ <br> <span class="text-[#c5a059]">A ROMÂNIEI</span>
            </h1>
            <p class="text-gray-400 text-[11px] uppercase tracking-widest mt-4">Identity Verification Required</p>
        </div>

        <div class="space-y-4 text-left">
            <div>
                <label class="text-[11px] text-gray-400 uppercase ml-1">Username</label>
                <input type="text" id="userInput" placeholder="Halimbawa: admin"
                    class="w-full p-3 border border-gray-200 rounded focus:border-[#c5a059] outline-none transition">
            </div>
            <div>
                <label class="text-[11px] text-gray-400 uppercase ml-1">Password</label>
                <input type="password" id="passInput" placeholder="••••••••"
                    class="w-full p-3 border border-gray-200 rounded focus:border-[#c5a059] outline-none transition">
            </div>
            <p id="errorMsg" class="text-red-500 text-xs hidden italic text-center">Nume de utilizator sau parolă incorectă!</p>
            
            <button onclick="checkLogin()" 
                class="w-full bg-[#003d7a] hover:bg-[#002147] text-white font-bold py-3 rounded mt-4 transition shadow-md">
                Login to NetBanking
            </button>
        </div>
    </div>

    <!-- 2. MFA VERIFICATION SECTION (Hidden by default) -->
    <div id="mfaOverlay" class="hidden fixed inset-0 bg-[#002147]/98 flex items-center justify-center">
        <div class="bg-white p-10 bnr-card rounded w-[400px] text-center">
            <div class="mb-4 flex justify-center">
                <span class="bg-blue-100 text-[#002147] p-3 rounded-full">🛡️</span>
            </div>
            <h2 class="text-[#002147] font-bold text-xl mb-2">Multi-Factor Authentication</h2>
            <p class="text-gray-500 text-sm mb-8 italic">Am trimis un cod de securitate pe dispozitivul dumneavoastră înregistrat.</p>
            
            <input type="text" id="mfaCode" placeholder="0 0 0 0 0 0" maxlength="6"
                class="w-full p-4 text-center text-3xl tracking-[10px] font-bold border-b-2 border-[#c5a059] outline-none mb-8">
            
            <button onclick="verifyMFA()" 
                class="w-full bg-[#c5a059] hover:bg-[#a38446] text-white py-3 font-bold rounded shadow-lg transition">
                CONFIRMĂ CODUL
            </button>
        </div>
    </div>

    <!-- 3. SUCCESS DASHBOARD (Para sa dulo ng demo) -->
    <div id="successPage" class="hidden text-center text-white">
        <h1 class="text-5xl font-bold mb-4 text-[#c5a059]">Bine ați venit!</h1>
        <p class="text-xl opacity-80 italic text-white">Accesul la contul BNR MFA Funds a fost autorizat.</p>
    </div>

    <script>
        // ACCOUNT DETAILS PARA SA DEMO
        const VALID_USER = "admin";
        const VALID_PASS = "bnr123";
        const VALID_MFA  = "123456";

        function checkLogin() {
            const user = document.getElementById('userInput').value;
            const pass = document.getElementById('passInput').value;
            const error = document.getElementById('errorMsg');

            if (user === VALID_USER && pass === VALID_PASS) {
                // Pag tama, itatago ang login card at ipapakita ang MFA
                document.getElementById('loginCard').classList.add('hidden');
                document.getElementById('mfaOverlay').classList.remove('hidden');
            } else {
                // Pag mali, lalabas ang error message
                error.classList.remove('hidden');
            }
        }

        function verifyMFA() {
            const code = document.getElementById('mfaCode').value;
            if (code === VALID_MFA) {
                document.getElementById('mfaOverlay').classList.add('hidden');
                document.getElementById('successPage').classList.remove('hidden');
            } else {
                alert("Cod MFA invalid! Vă rugăm să încercați din nou.");
            }
        }
    </script>

</body>
</html>
