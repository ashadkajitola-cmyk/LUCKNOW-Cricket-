<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Schedule & Points Table Portal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .hidden-section { display: none; }
    </style>
</head>
<body class="bg-slate-100 font-sans text-gray-800">

    <!-- Navbar -->
    <nav class="bg-emerald-700 text-white p-4 shadow-md flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img id="nav-avatar" src="" alt="" class="w-9 h-9 rounded-full object-cover border-2 border-white hidden-section">
            <h1 class="text-xl font-bold">🏏 Cricket Portal</h1>
        </div>
        <div id="nav-user-info" class="flex items-center gap-4 hidden-section">
            <span id="nav-phone" class="text-sm bg-emerald-800 px-3 py-1 rounded"></span>
            <span id="nav-wallet" class="text-sm bg-amber-500 text-slate-900 font-bold px-3 py-1 rounded"></span>
            <button onclick="logout()" class="bg-red-600 px-3 py-1 text-sm rounded hover:bg-red-700">Logout</button>
        </div>
    </nav>

    <div class="container mx-auto p-4 max-w-5xl">

        <!-- 1. LOGIN SECTION -->
        <div id="login-section" class="bg-white p-6 rounded-lg shadow-md max-w-md mx-auto mt-10">
            <h2 class="text-2xl font-bold text-center mb-4 text-emerald-700">Login / Register</h2>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Mobile Number:</label>
                <input type="text" id="login-phone" placeholder="Enter Mobile Number" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Aapka Naam (Required):</label>
                <input type="text" id="login-name" placeholder="Enter Your Name" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Profile Photo URL (Optional - Skip kar sakte hain):</label>
                <input type="text" id="login-photo" placeholder="https://example.com/photo.jpg" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <div class="mb-4">
                <label class="block text-sm font-medium mb-1">Unique User ID (Exactly 5 letters/chars):</label>
                <input type="text" id="login-userid" maxlength="5" placeholder="e.g. df43h" class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
            </div>
            <button onclick="handleLogin()" class="w-full bg-emerald-600 text-white py-2 rounded font-bold hover:bg-emerald-700">Login / Register</button>
            <p class="text-xs text-emerald-600 mt-3 text-center font-semibold">✨ New user bonus: ₹25 Free Wallet Cash + 30 Mins Free Subscription!</p>
            <p class="text-xs text-gray-500 mt-1 text-center">Note: Special number `9569981484` ko master admin access milta hai!</p>
        </div>

        <!-- 2. MAIN DASHBOARD -->
        <div id="dashboard-section" class="hidden-section">
            <!-- Tabs -->
            <div class="flex flex-wrap gap-2 mb-6 border-b pb-2">
                <button onclick="switchTab('matches')" class="px-4 py-2 bg-emerald-600 text-white rounded font-medium tab-btn" id="btn-matches">Match Schedule</button>
                <button onclick="switchTab('points')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-points">Points Table</button>
                <button onclick="switchTab('subscription')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-subscription">Subscriptions</button>
                <button onclick="switchTab('earn')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-earn">Mehnat Karo (Earn ₹)</button>
                <button onclick="switchTab('admin')" class="px-4 py-2 bg-gray-200 text-gray-700 rounded font-medium tab-btn" id="btn-admin">Admin Panel</button>
            </div>

            <!-- TAB 1: MATCH SCHEDULE -->
            <div id="tab-matches" class="space-y-4">
                <h3 id="schedule-series-title" class="text-xl font-bold text-emerald-800">Scheduled Matches</h3>
                <div id="matches-list" class="space-y-4"></div>
            </div>

            <!-- TAB 2: POINTS TABLE -->
            <div id="tab-points" class="hidden-section space-y-6">
                <h3 class="text-xl font-bold text-emerald-800">ICC Points Table</h3>
                <div id="points-tables-container" class="space-y-6"></div>
            </div>

            <!-- TAB 3: SUBSCRIPTION -->
            <div id="tab-subscription" class="hidden-section bg-white p-6 rounded-lg shadow-md">
                <h3 class="text-xl font-bold mb-4 text-emerald-800">Active Subscription Status</h3>
                <div id="subscription-status" class="mb-6 p-4 bg-amber-50 border border-amber-200 rounded"></div>
                
                <h4 class="text-lg font-semibold mb-3">Buy Subscription (Deduct from Wallet Balance in ₹)</h4>
                <p class="text-xs text-gray-500 mb-4">Official Merchant UPI Support & Central Revenue: <span class="font-bold text-emerald-700">9120468311</span></p>

                <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">30 Minutes Subscription</p>
                        <p class="text-sm text-gray-600">Cost: ₹15</p>
                        <button onclick="buySubscription('30min', 15)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Half Monthly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: ₹199</p>
                        <button onclick="buySubscription('half_monthly', 199)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Monthly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: ₹349</p>
                        <button onclick="buySubscription('monthly', 349)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm">
                        <p class="font-bold">Half Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: ₹1499</p>
                        <button onclick="buySubscription('half_yearly', 1499)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                    <div class="p-4 border rounded shadow-sm col-span-full">
                        <p class="font-bold">Yearly Subscription</p>
                        <p class="text-sm text-gray-600">Cost: ₹2499</p>
                        <button onclick="buySubscription('yearly', 2499)" class="mt-2 bg-blue-600 text-white px-3 py-1 rounded text-sm">Buy Now</button>
                    </div>
                </div>
            </div>

            <!-- TAB: EARN MONEY (NEW TASKS) -->
            <div id="tab-earn" class="hidden-section bg-white p-6 rounded-lg shadow-md max-w-lg mx-auto space-y-6">
                <div>
                    <h3 class="text-xl font-bold mb-2 text-emerald-800">🧠 Cricket Trivia Challenge (Earn ₹10)</h3>
                    <p class="text-sm text-gray-600 mb-4">Sawal ka sahi jawab dekar turant apne wallet me ₹10 jeetein!</p>
                    <div class="bg-emerald-50 p-4 rounded text-center mb-4 border border-emerald-200">
                        <span id="trivia-question" class="text-base font-bold text-emerald-900 block"></span>
                    </div>
                    <div class="mb-4">
                        <input type="text" id="user-trivia-answer" placeholder="Enter answer here..." class="w-full p-2 border rounded focus:ring-2 focus:ring-emerald-500">
                    </div>
                    <button onclick="verifyTriviaAnswer()" class="w-full bg-emerald-600 text-white py-2 rounded font-bold hover:bg-emerald-700">Submit & Win ₹10</button>
                </div>

                <hr class="border-dashed">

                <!-- New Earning Option: Match Winner Predictor -->
                <div>
                    <h3 class="text-xl font-bold mb-2 text-emerald-800">🎯 Match Predictor Task (Earn ₹15)</h3>
                    <p class="text-sm text-gray-600 mb-4">Aane wale match me kaunsi team jitegi guess karein!</p>
                    <div class="mb-3">
                        <label class="block text-sm font-medium mb-1">Select Match:</label>
                        <select id="earn-match-select" class="w-full p-2 border rounded"></select>
                    </div>
                    <div class="mb-3">
                        <label class="block text-sm font-medium mb-1">Aapki Winning Team Guess:</label>
                        <input type="text" id="user-prediction-team" placeholder="Team name..." class="w-full p-2 border rounded">
                    </div>
                    <button onclick="submitPrediction()" class="w-full bg-blue-600 text-white py-2 rounded font-bold hover:bg-blue-700">Lock Prediction & Earn ₹15</button>
                </div>
            </div>

            <!-- TAB 4: ADMIN PANEL -->
            <div id="tab-admin" class="hidden-section space-y-6">
                <div class="bg-white p-6 rounded-lg shadow-md border-t-4 border-emerald-600">
                    <h3 class="text-xl font-bold text-emerald-800 mb-4">👑 Admin Panel</h3>

                    <!-- Schedule Match Form -->
                    <div class="border-b pb-6 mb-6">
                        <h4 id="form-heading" class="font-semibold mb-3 text-lg">Schedule New Match</h4>
                        <input type="hidden" id="edit-match-index" value="-1">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm">Series Type:</label>
                                <select id="admin-series-type" class="w-full p-2 border rounded">
                                    <option value="existing">Same Series Match</option>
                                    <option value="new">New Series Match (New Gap)</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Series Name:</label>
                                <input type="text" id="admin-series-name" placeholder="Series Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Label:</label>
                                <input type="text" id="admin-match-label" placeholder="1st T20" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Group Name:</label>
                                <input type="text" id="admin-group-name" placeholder="Group Name" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Match Date & Time Tag:</label>
                                <input type="date" id="admin-date" class="w-full p-2 border rounded mb-2">
                                <input type="text" id="admin-time" placeholder="Time or Extra Tag" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 1 & Score:</label>
                                <input type="text" id="admin-team1" placeholder="Team 1 Name" class="w-full p-2 border rounded mb-2">
                                <input type="text" id="admin-score1" placeholder="Score info" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 2 & Score:</label>
                                <input type="text" id="admin-team2" placeholder="Team 2 Name" class="w-full p-2 border rounded mb-2">
                                <input type="text" id="admin-score2" placeholder="Score info" class="w-full p-2 border rounded">
                            </div>
                            <div class="col-span-full">
                                <label class="block text-sm">Venue:</label>
                                <input type="text" id="admin-venue" placeholder="Stadium / Venue" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <div class="flex gap-2 mt-4">
                            <button id="save-match-btn" onclick="scheduleMatch()" class="bg-emerald-600 text-white px-4 py-2 rounded font-bold hover:bg-emerald-700">Publish / Schedule Match</button>
                            <button id="cancel-edit-btn" onclick="resetMatchForm()" class="hidden-section bg-gray-500 text-white px-4 py-2 rounded font-bold hover:bg-gray-600">Cancel Edit</button>
                        </div>
                    </div>

                    <!-- Manage Matches -->
                    <div class="border-b pb-6 mb-6">
                        <h4 class="font-semibold mb-3 text-lg">Manage Existing Matches</h4>
                        <div id="admin-matches-manage-list" class="space-y-2 max-h-60 overflow-y-auto border p-2 rounded"></div>
                    </div>

                    <!-- Points Table Updater -->
                    <div class="border-b pb-6 mb-6">
                        <h4 class="font-semibold mb-3 text-lg">Update Points Table (ICC Formula)</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                            <div>
                                <label class="block text-sm">Select Group:</label>
                                <select id="update-group-select" onchange="onGroupSelectChange()" class="w-full p-2 border rounded">
                                    <option value="">-- Choose Group --</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Match Result:</label>
                                <select id="admin-match-outcome" class="w-full p-2 border rounded">
                                    <option value="team1_win">Team 1 Wins</option>
                                    <option value="team2_win">Team 2 Wins</option>
                                    <option value="tied">Tied</option>
                                    <option value="nr">No Result / Abandoned</option>
                                </select>
                            </div>
                            <div>
                                <label class="block text-sm">Team 1 Details:</label>
                                <select id="update-team1-select" class="w-full p-2 border rounded mb-2"></select>
                                <input type="number" id="admin-team1-runs" placeholder="Runs Scored" class="w-full p-2 border rounded mb-2">
                                <input type="number" step="0.1" id="admin-team1-overs" placeholder="Overs Faced" class="w-full p-2 border rounded">
                            </div>
                            <div>
                                <label class="block text-sm">Team 2 Details:</label>
                                <select id="update-team2-select" class="w-full p-2 border rounded mb-2"></select>
                                <input type="number" id="admin-team2-runs" placeholder="Runs Scored" class="w-full p-2 border rounded mb-2">
                                <input type="number" step="0.1" id="admin-team2-overs" placeholder="Overs Faced" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="updatePointsTableICC()" class="bg-blue-600 text-white px-4 py-2 rounded font-bold hover:bg-blue-700">Update Points Table</button>
                    </div>

                    <!-- Admin Cash Sender -->
                    <div>
                        <h4 class="font-semibold mb-3 text-lg">Send Money (₹) Directly (Admin Only)</h4>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label class="block text-sm">User ID or Mobile:</label>
                                <input type="text" id="admin-send-userid" placeholder="Enter User ID or Mobile" oninput="checkRecipientUser()" class="w-full p-2 border rounded">
                                <span id="recipient-status" class="text-xs font-semibold mt-1 block"></span>
                            </div>
                            <div>
                                <label class="block text-sm">Amount in ₹:</label>
                                <input type="number" id="admin-send-amount" placeholder="Amount to send" class="w-full p-2 border rounded">
                            </div>
                        </div>
                        <button onclick="adminSendMoney()" class="mt-4 bg-amber-600 text-white px-4 py-2 rounded font-bold hover:bg-amber-700">Send Money</button>
                    </div>

                </div>
            </div>

        </div>

    </div>

    <!-- JavaScript Logic -->
    <script>
        const DB_KEY = "cricket_portal_db_v13";
        const MERCHANT_UPI = "9120468311";
        let currentUserPhone = localStorage.getItem("current_logged_user") || null;
        let currentDeviceId = localStorage.getItem("device_id");
        let currentTrivia = { question: "", answer: "" };

        if (!currentDeviceId) {
            currentDeviceId = "dev_" + Math.random().toString(36).substring(2, 9);
            localStorage.setItem("device_id", currentDeviceId);
        }

        const triviaPool = [
            { q: "Who won the ICC Men's T20 World Cup in 2024? (India / South Africa)", a: "india" },
            { q: "How many players are on the field for one team in a cricket match?", a: "11" },
            { q: "Which country hosts the headquarters of the ICC? (UAE / India / England)", a: "uae" },
            { q: "What is the maximum number of overs per bowler in a standard ODI match?", a: "10" },
            { q: "Which format is known as the longest format of international cricket?", a: "test" }
        ];

        function getDB() {
            let data = localStorage.getItem(DB_KEY);
            if (!data) {
                let initial = {
                    users: {},       
                    userIDs: {},     
                    devices: {},
                    matches: [],
                    pointsTable: {},
                    subscriptionLogs: [] // Centralized tracking for 9120468311
                };
                // Ensure merchant account exists
                initial.users[MERCHANT_UPI] = {
                    phone: MERCHANT_UPI,
                    name: "Merchant Central",
                    userid: "merch",
                    wallet: 40,
                    subscription: { activeUntil: new Date().getTime() + (999 * 24 * 60 * 60 * 1000) }
                };
                initial.userIDs["merch"] = { phone: MERCHANT_UPI, wallet: 40 };
                
                localStorage.setItem(DB_KEY, JSON.stringify(initial));
                return initial;
            }
            let db = JSON.parse(data);
            if (!db.subscriptionLogs) db.subscriptionLogs = [];
            if (!db.users[MERCHANT_UPI]) {
                db.users[MERCHANT_UPI] = { phone: MERCHANT_UPI, name: "Merchant", userid: "merch", wallet: 40, subscription: { activeUntil: 9999999999999 } };
            }
            return db;
        }

        function saveDB(db) {
            localStorage.setItem(DB_KEY, JSON.stringify(db));
        }

        window.onload = function() {
            if (currentUserPhone) {
                let db = getDB();
                if (db.users[currentUserPhone]) {
                    initDashboard();
                } else {
                    currentUserPhone = null;
                    localStorage.removeItem("current_logged_user");
                }
            }
            loadNewTrivia();
            populateEarnMatches();
        };

        function loadNewTrivia() {
            let rand = triviaPool[Math.floor(Math.random() * triviaPool.length)];
            currentTrivia = rand;
            let qElem = document.getElementById("trivia-question");
            if(qElem) qElem.innerText = currentTrivia.q;
        }

        function verifyTriviaAnswer() {
            let userAns = document.getElementById("user-trivia-answer").value.trim().toLowerCase();
            if (!userAns) {
                alert("Kripya apna jawab likhein!");
                return;
            }

            if (!userAns.includes(currentTrivia.answer)) {
                alert("Galat jawab! Phir se koshish karein.");
                document.getElementById("user-trivia-answer").value = "";
                loadNewTrivia();
                return;
            }

            let db = getDB();
            let user = db.users[currentUserPhone];

            user.wallet += 10; 
            if (db.userIDs[user.userid]) {
                db.userIDs[user.userid].wallet = user.wallet;
            }

            saveDB(db);
            alert("Sahi jawab! Aapke wallet me ₹10 jud gaye hain.");
            document.getElementById("user-trivia-answer").value = "";
            loadNewTrivia();
            initDashboard();
        }

        function populateEarnMatches() {
            let db = getDB();
            let select = document.getElementById("earn-match-select");
            if (!select) return;
            select.innerHTML = "";
            if (db.matches.length === 0) {
                select.innerHTML = `<option value="">No matches available</option>`;
                return;
            }
            db.matches.forEach(m => {
                select.innerHTML += `<option value="${m.team1} vs ${m.team2}">${m.matchLabel}: ${m.team1} vs ${m.team2}</option>`;
            });
        }

        function submitPrediction() {
            let predTeam = document.getElementById("user-prediction-team").value.trim();
            if (!predTeam) {
                alert("Kripya apni winning team ka naam likhein!");
                return;
            }
            let db = getDB();
            let user = db.users[currentUserPhone];
            user.wallet += 15;
            if (db.userIDs[user.userid]) {
                db.userIDs[user.userid].wallet = user.wallet;
            }
            saveDB(db);
            alert("Prediction locked! Aapke wallet me ₹15 credit kar diye gaye hain.");
            document.getElementById("user-prediction-team").value = "";
            initDashboard();
        }

        function handleLogin() {
            let phone = document.getElementById("login-phone").value.trim();
            let name = document.getElementById("login-name").value.trim();
            let photo = document.getElementById("login-photo").value.trim();
            let userid = document.getElementById("login-userid").value.trim().toLowerCase();

            if (!phone || !userid || !name) {
                alert("Kripya Mobile Number, Naam aur User ID sabhi fields bharein.");
                return;
            }

            if (userid.length !== 5) {
                alert("User ID must be exactly 5 letters/characters long.");
                return;
            }

            let db = getDB();

            if (db.userIDs[userid] && db.userIDs[userid].phone && db.userIDs[userid].phone !== "Pending Login" && db.userIDs[userid].phone !== phone) {
                alert("This User ID is already registered with another mobile number!");
                return;
            }

            if (!db.devices[currentDeviceId]) {
                db.devices[currentDeviceId] = [];
            }

            let devicePhones = db.devices[currentDeviceId];
            if (!devicePhones.includes(phone) && devicePhones.length >= 4) {
                alert("Maximum 4 numbers allowed per device!");
                return;
            }

            // Check if another user is already logged in on this device
            if (devicePhones.length > 0 && !devicePhones.includes(phone) && currentUserPhone) {
                alert("Pehle wale user ko logout karein, tabhi naye number se login kar sakenge!");
                return;
            }

            let isNewUser = false;
            if (!db.users[phone]) {
                isNewUser = true;
                db.users[phone] = {
                    phone: phone,
                    name: name,
                    photo: photo || "",
                    userid: userid,
                    wallet: 25, 
                    subscription: { activeUntil: new Date().getTime() + (30 * 60 * 1000) } 
                };
            } else {
                db.users[phone].name = name;
                if(photo) db.users[phone].photo = photo;
                if (db.users[phone].wallet === undefined) db.users[phone].wallet = 0;
                if (!db.users[phone].subscription) db.users[phone].subscription = { activeUntil: 0 };
            }

            let userObj = db.users[phone];

            if (!db.userIDs[userid]) {
                db.userIDs[userid] = { phone: phone, wallet: userObj.wallet };
            } else {
                db.userIDs[userid].phone = phone;
                db.userIDs[userid].wallet = Math.max(db.userIDs[userid].wallet, userObj.wallet);
                userObj.wallet = db.userIDs[userid].wallet;
            }

            if (!devicePhones.includes(phone)) {
                devicePhones.push(phone);
            }

            saveDB(db);
            currentUserPhone = phone;
            localStorage.setItem("current_logged_user", currentUserPhone);
            
            if (isNewUser) {
                alert("Welcome! Aapko naye user hone par ₹25 bonus aur 30 minutes ki free subscription mil gayi hai!");
            }

            initDashboard();
        }

        function logout() {
            currentUserPhone = null;
            localStorage.removeItem("current_logged_user");
            document.getElementById("login-section").classList.remove("hidden-section");
            document.getElementById("dashboard-section").classList.add("hidden-section");
            document.getElementById("nav-user-info").classList.add("hidden-section");
            document.getElementById("nav-avatar").classList.add("hidden-section");
        }

        function initDashboard() {
            document.getElementById("login-section").classList.add("hidden-section");
            document.getElementById("dashboard-section").classList.remove("hidden-section");
            document.getElementById("nav-user-info").classList.remove("hidden-section");

            let db = getDB();
            let user = db.users[currentUserPhone];

            if (user && db.userIDs[user.userid]) {
                user.wallet = db.userIDs[user.userid].wallet;
            }

            let avatarElem = document.getElementById("nav-avatar");
            if (user.photo) {
                avatarElem.src = user.photo;
                avatarElem.classList.remove("hidden-section");
            } else {
                avatarElem.classList.add("hidden-section");
            }

            document.getElementById("nav-phone").innerText = `📞 ${user.name} (${user.userid.toUpperCase()})`;
            document.getElementById("nav-wallet").innerText = `💰 Wallet: ₹${user.wallet}`;

            renderMatches();
            renderPointsTable();
            renderSubscriptionStatus();
            renderAdminManageMatches();
            populateGroupDropdowns();
            populateEarnMatches();
        }

        function switchTab(tabName) {
            let db = getDB();
            let now = new Date().getTime();
            let user = db.users[currentUserPhone];
            let userSubActive = user && user.subscription && user.subscription.activeUntil > now;
            
            let isAdminActive = (currentUserPhone === "9569981484") || userSubActive;

            if (tabName === 'admin' && !isAdminActive) {
                alert("Access Denied! Admin panel keval 9569981484 (Master Admin) ya active subscription wale numbers ke liye hi open hoga.");
                return;
            }

            ['matches', 'points', 'subscription', 'earn', 'admin'].forEach(t => {
                let tabElem = document.getElementById(`tab-${t}`);
                let btnElem = document.getElementById(`btn-${t}`);
                if(tabElem) tabElem.classList.add("hidden-section");
                if(btnElem) {
                    btnElem.classList.remove("bg-emerald-600", "text-white");
                    btnElem.classList.add("bg-gray-200", "text-gray-700");
                }
            });

            document.getElementById(`tab-${tabName}`).classList.remove("hidden-section");
            document.getElementById(`btn-${tabName}`).classList.remove("bg-gray-200", "text-gray-700");
            document.getElementById(`btn-${tabName}`).classList.add("bg-emerald-600", "text-white");
            
            if(tabName === 'admin') {
                renderAdminManageMatches();
                populateGroupDropdowns();
            }
        }

        function buySubscription(plan, cost) {
            let db = getDB();
            let user = db.users[currentUserPhone];

            let currentWallet = user ? user.wallet : 0;
            if (user && db.userIDs[user.userid]) {
                currentWallet = db.userIDs[user.userid].wallet;
            }

            if (currentWallet < cost) {
                alert(`Wallet me paryaapt paise nahi hain! Aapko ₹${cost} chahiye. 'Mehnat Karo' tab me jaakar paise kamayein.`);
                return;
            }

            // Deduct from user wallet
            currentWallet -= cost;
            if (user) user.wallet = currentWallet;
            if (user && db.userIDs[user.userid]) db.userIDs[user.userid].wallet = currentWallet;

            // Route money to 9120468311 merchant account
            if (db.users[MERCHANT_UPI]) {
                db.users[MERCHANT_UPI].wallet += cost;
                if(db.userIDs["merch"]) db.userIDs["merch"].wallet = db.users[MERCHANT_UPI].wallet;
            }

            let durationMs = 0;
            if (plan === '30min') durationMs = 30 * 60 * 1000;
            else if (plan === 'half_monthly') durationMs = 15 * 24 * 60 * 60 * 1000;
            else if (plan === 'monthly') durationMs = 30 * 24 * 60 * 60 * 1000;
            else if (plan === 'half_yearly') durationMs = 182 * 24 * 60 * 60 * 1000;
            else if (plan === 'yearly') durationMs = 365 * 24 * 60 * 60 * 1000;

            let now = new Date().getTime();
            if (!user.subscription) user.subscription = { activeUntil: 0 };

            if (user.subscription.activeUntil > now) {
                user.subscription.activeUntil += durationMs;
            } else {
                user.subscription.activeUntil = now + durationMs;
            }

            let expireTimeStr = new Date(user.subscription.activeUntil).toLocaleString();

            // Ask rating 1 to 5 stars
            let ratingInput = prompt("Subscription successfully bought! Kripya is service ko 1 se 5 star tak rate karein:", "5");
            let starRating = parseInt(ratingInput) || 5;
            if(starRating < 1) starRating = 1;
            if(starRating > 5) starRating = 5;

            // Save details to merchant 9120468311 logs
            db.subscriptionLogs.push({
                userPhone: currentUserPhone,
                userName: user.name,
                plan: plan,
                cost: cost,
                rating: starRating,
                expiresAt: expireTimeStr,
                timestamp: new Date().toLocaleString()
            });

            saveDB(db);
            alert(`Subscription safaltapurvak activate ho gayi hai! Details Merchant number ${MERCHANT_UPI} par bhej di gayi hain.`);
            initDashboard();
        }

        function renderSubscriptionStatus() {
            let db = getDB();
            let now = new Date().getTime();
            let user = db.users[currentUserPhone];
            let statusBox = document.getElementById("subscription-status");

            if (currentUserPhone === "9569981484") {
                statusBox.innerHTML = `<p class="text-emerald-700 font-bold">Status: Master Admin (${currentUserPhone})</p><p class="text-sm">Aapka account hamesha ke liye free aur active hai.</p>`;
                return;
            }

            let subActiveUntil = user && user.subscription ? user.subscription.activeUntil : 0;
            if (subActiveUntil > now) {
                let timeLeft = Math.ceil((subActiveUntil - now) / (1000 * 60));
                statusBox.innerHTML = `<p class="text-emerald-700 font-bold">Status: Active</p><p class="text-sm">Expires in approximately ${timeLeft} minutes.</p>`;
            } else {
                statusBox.innerHTML = `<p class="text-red-600 font-bold">Status: Inactive</p><p class="text-sm">Is number par subscription active nahi hai. Nayi subscription khareedne ke liye wallet balance use karein.</p>`;
            }
        }

        function scheduleMatch() {
            let db = getDB();
            let now = new Date().getTime();
            let user = db.users[currentUserPhone];
            let userSubActive = user && user.subscription && user.subscription.activeUntil > now;

            if (currentUserPhone !== "9569981484" && !userSubActive) {
                alert("Access Denied! Aapke number par admin permissions nahi hain.");
                return;
            }

            let editIndex = parseInt(document.getElementById("edit-match-index").value);
            let seriesType = document.getElementById("admin-series-type").value;
            let seriesName = document.getElementById("admin-series-name").value.trim();
            let matchLabel = document.getElementById("admin-match-label").value.trim() || "Match";
            let groupName = document.getElementById("admin-group-name").value.trim() || "General Group";
            let team1 = document.getElementById("admin-team1").value.trim();
            let team2 = document.getElementById("admin-team2").value.trim();
            let score1 = document.getElementById("admin-score1").value.trim() || "Yet to bat";
            let score2 = document.getElementById("admin-score2").value.trim() || "Yet to bat";
            let date = document.getElementById("admin-date").value;
            let time = document.getElementById("admin-time").value;
            let venue = document.getElementById("admin-venue").value.trim();

            if (!team1 || !team2 || !date || !venue || !seriesName) {
                alert("Please fill all required match details.");
                return;
            }

            let matchData = { seriesType, seriesName, matchLabel, groupName, team1, team2, score1, score2, date, time, venue };

            if (editIndex === -1) {
                db.matches.push(matchData);
                alert("Match scheduled successfully!");
            } else {
                db.matches[editIndex] = matchData;
                alert("Match updated successfully!");
                resetMatchForm();
            }

            if (!db.pointsTable[groupName]) {
                db.pointsTable[groupName] = [];
            }
            [team1, team2].forEach(tName => {
                if (!db.pointsTable[groupName].some(t => t.team.toLowerCase() === tName.toLowerCase())) {
                    db.pointsTable[groupName].push({ team: tName, p: 0, w: 0, l: 0, t: 0, pts: 0, nrr: 0.0, runsFor: 0, oversFor: 0, runsAgainst: 0, oversAgainst: 0 });
                }
            });

            saveDB(db);
            renderMatches();
            renderPointsTable();
            renderAdminManageMatches();
            populateGroupDropdowns();
            populateEarnMatches();
            switchTab("matches");
        }

        function renderMatches() {
            let db = getDB();
            let container = document.getElementById("matches-list");
            let seriesTitleElem = document.getElementById("schedule-series-title");
            container.innerHTML = "";

            if (db.matches.length === 0) {
                seriesTitleElem.innerText = "Scheduled Matches";
                container.innerHTML = `<p class="text-gray-500">No matches scheduled yet.</p>`;
                return;
            }

            seriesTitleElem.innerText = db.matches[db.matches.length - 1].seriesName;

            let lastSeries = "";
            db.matches.forEach((m, idx) => {
                let showGap = m.seriesType === 'new' || (idx > 0 && m.seriesName !== lastSeries);
                lastSeries = m.seriesName;

                let html = "";
                if (showGap && idx > 0) {
                    html += `<div class="my-6 border-t-2 border-dashed border-emerald-500"></div>`;
                }

                html += `
                    <div class="bg-white p-4 rounded-lg shadow-sm border border-gray-200">
                        <div class="flex justify-between items-center text-xs text-gray-500 mb-1">
                            <span class="font-bold text-emerald-800">${m.matchLabel}</span>
                            <span>📅 ${m.date} | ⏰ ${m.time}</span>
                        </div>
                        <div class="flex justify-between items-center my-2">
                            <div class="text-base font-bold text-gray-800 flex items-center gap-2">🏏 ${m.team1} <span class="text-xs font-normal text-gray-500">(${m.score1})</span></div>
                            <span class="text-sm font-bold text-gray-400">vs</span>
                            <div class="text-base font-bold text-gray-800 text-right flex items-center justify-end gap-2"><span class="text-xs font-normal text-gray-500">(${m.score2})</span> ${m.team2} 🏏</div>
                        </div>
                        <p class="text-xs text-gray-600 mt-2">📍 Venue: ${m.venue}</p>
                    </div>
                `;
                container.innerHTML += html;
            });
        }

        function renderAdminManageMatches() {
            let db = getDB();
            let listContainer = document.getElementById("admin-matches-manage-list");
            listContainer.innerHTML = "";

            if (db.matches.length === 0) {
                listContainer.innerHTML = `<p class="text-xs text-gray-500">No matches available to manage.</p>`;
                return;
            }

            db.matches.forEach((m, idx) => {
                listContainer.innerHTML += `
                    <div class="flex justify-between items-center bg-gray-50 p-2 rounded border text-sm">
                        <div>
                            <span class="font-bold">${m.matchLabel}:</span> ${m.team1} vs ${m.team2} <span class="text-xs text-gray-500">(${m.seriesName})</span>
                        </div>
                        <div class="flex gap-2">
                            <button onclick="editMatch(${idx})" class="bg-blue-500 text-white px-2 py-1 text-xs rounded hover:bg-blue-600">Edit</button>
                            <button onclick="deleteMatch(${idx})" class="bg-red-500 text-white px-2 py-1 text-xs rounded hover:bg-red-600">Delete</button>
                        </div>
                    </div>
                `;
            });
        }

        function editMatch(idx) {
            let db = getDB();
            let m = db.matches[idx];

            document.getElementById("edit-match-index").value = idx;
            document.getElementById("admin-series-type").value = m.seriesType;
            document.getElementById("admin-series-name").value = m.seriesName;
            document.getElementById("admin-match-label").value = m.matchLabel;
            document.getElementById("admin-group-name").value = m.groupName;
            document.getElementById("admin-date").value = m.date;
            document.getElementById("admin-time").value = m.time;
            document.getElementById("admin-team1").value = m.team1;
            document.getElementById("admin-score1").value = m.score1;
            document.getElementById("admin-team2").value = m.team2;
            document.getElementById("admin-score2").value = m.score2;
            document.getElementById("admin-venue").value = m.venue;

            document.getElementById("form-heading").innerText = "Edit Scheduled Match";
            document.getElementById("save-match-btn").innerText = "Update Match";
            document.getElementById("cancel-edit-btn").classList.remove("hidden-section");
        }

        function resetMatchForm() {
            document.getElementById("edit-match-index").value = "-1";
            document.getElementById("admin-series-name").value = "";
            document.getElementById("admin-match-label").value = "";
            document.getElementById("admin-group-name").value = "";
            document.getElementById("admin-date").value = "";
            document.getElementById("admin-time").value = "";
            document.getElementById("admin-team1").value = "";
            document.getElementById("admin-score1").value = "";
            document.getElementById("admin-team2").value = "";
            document.getElementById("admin-score2").value = "";
            document.getElementById("admin-venue").value = "";

            document.getElementById("form-heading").innerText = "Schedule New Match";
            document.getElementById("save-match-btn").innerText = "Publish / Schedule Match";
            document.getElementById("cancel-edit-btn").classList.add("hidden-section");
        }

        function deleteMatch(idx) {
            let db = getDB();
            let now = new Date().getTime();
            let user = db.users[currentUserPhone];
            let userSubActive = user && user.subscription && user.subscription.activeUntil > now;

            if (currentUserPhone !== "9569981484" && !userSubActive) {
                alert("Access Denied!");
                return;
            }

            if (confirm("Are you sure you want to delete this match?")) {
                db.matches.splice(idx, 1);
                saveDB(db);
                renderMatches();
                renderAdminManageMatches();
                populateEarnMatches();
                alert("Match deleted successfully!");
            }
        }

        function populateGroupDropdowns() {
            let db = getDB();
            let groupSelect = document.getElementById("update-group-select");
            groupSelect.innerHTML = `<option value="">-- Choose Group --</option>`;

            Object.keys(db.pointsTable).forEach(group => {
                groupSelect.innerHTML += `<option value="${group}">${group} (${db.pointsTable[group].length} teams)</option>`;
            });
        }

        function onGroupSelectChange() {
            let db = getDB();
            let group = document.getElementById("update-group-select").value;
            let t1Select = document.getElementById("update-team1-select");
            let t2Select = document.getElementById("update-team2-select");

            t1Select.innerHTML = `<option value="">-- Select Team 1 --</option>`;
            t2Select.innerHTML = `<option value="">-- Select Team 2 --</option>`;

            if (!group || !db.pointsTable[group]) return;

            db.pointsTable[group].forEach(t => {
                t1Select.innerHTML += `<option value="${t.team}">${t.team}</option>`;
                t2Select.innerHTML += `<option value="${t.team}">${t.team}</option>`;
            });
        }

        function updatePointsTableICC() {
            let db = getDB();
            let now = new Date().getTime();
            let user = db.users[currentUserPhone];
            let userSubActive = user && user.subscription && user.subscription.activeUntil > now;

            if (currentUserPhone !== "9569981484" && !userSubActive) {
                alert("Access Denied! Aapke number par admin permissions nahi hain.");
                return;
            }

            let group = document.getElementById("update-group-select").value;
            let outcome = document.getElementById("admin-match-outcome").value;
            let team1Name = document.getElementById("update-team1-select").value;
            let team2Name = document.getElementById("update-team2-select").value;

            let runs1 = parseFloat(document.getElementById("admin-team1-runs").value) || 0;
            let overs1 = parseFloat(document.getElementById("admin-team1-overs").value) || 0;
            let runs2 = parseFloat(document.getElementById("admin-team2-runs").value) || 0;
            let overs2 = parseFloat(document.getElementById("admin-team2-overs").value) || 0;

            if (!group || !team1Name || !team2Name) {
                alert("Please select a group and both teams.");
                return;
            }

            if (team1Name === team2Name) {
                alert("Team 1 and Team 2 cannot be the same!");
                return;
            }

            let teamsList = db.pointsTable[group];
            let t1Obj = teamsList.find(t => t.team === team1Name);
            let t2Obj = teamsList.find(t => t.team === team2Name);

            if (!t1Obj || !t2Obj) {
                alert("Selected teams not found in points table.");
                return;
            }

            [t1Obj, t2Obj].forEach(t => {
                if(t.runsFor === undefined) t.runsFor = 0;
                if(t.oversFor === undefined) t.oversFor = 0;
                if(t.runsAgainst === undefined) t.runsAgainst = 0;
                if(t.oversAgainst === undefined) t.oversAgainst = 0;
            });

            t1Obj.p += 1;
            t2Obj.p += 1;

            if (outcome === 'team1_win') {
                t1Obj.w += 1; t1Obj.pts += 2;
                t2Obj.l += 1;
            } else if (outcome === 'team2_win') {
                t2Obj.w += 1; t2Obj.pts += 2;
                t1Obj.l += 1;
            } else if (outcome === 'tied') {
                t1Obj.t += 1; t1Obj.pts += 1;
                t2Obj.t += 1; t2Obj.pts += 1;
            } else if (outcome === 'nr') {
                t1Obj.t += 1; t1Obj.pts += 1;
                t2Obj.t += 1; t2Obj.pts += 1;
            }

            t1Obj.runsFor += runs1;
            t1Obj.oversFor += overs1;
            t1Obj.runsAgainst += runs2;
            t1Obj.oversAgainst += overs2;

            t2Obj.runsFor += runs2;
            t2Obj.oversFor += overs2;
            t2Obj.runsAgainst += runs1;
            t2Obj.oversAgainst += overs1;

            [t1Obj, t2Obj].forEach(t => {
                let scoredRate = t.oversFor > 0 ? (t.runsFor / t.oversFor) : 0;
                let concededRate = t.oversAgainst > 0 ? (t.runsAgainst / t.oversAgainst) : 0;
                t.nrr = parseFloat((scoredRate - concededRate).toFixed(3));
            });

            saveDB(db);
            alert("Points Table updated successfully via ICC Formula!");
            renderPointsTable();
        }

        function renderPointsTable() {
            let db = getDB();
            let container = document.getElementById("points-tables-container");
            container.innerHTML = "";

            let groupKeys = Object.keys(db.pointsTable);
            if (groupKeys.length === 0) {
                container.innerHTML = `<p class="text-gray-500">No groups or points tables created yet.</p>`;
                return;
            }

            groupKeys.forEach(group => {
                let teams = db.pointsTable[group].sort((a, b) => b.pts - a.pts || b.nrr - a.nrr);
                let rows = "";
                teams.forEach((t, i) => {
                    rows += `
                        <tr class="border-b text-center">
                            <td class="p-2 text-left">${i + 1}. ${t.team}</td>
                            <td class="p-2">${t.p}</td>
                            <td class="p-2">${t.w}</td>
                            <td class="p-2">${t.l}</td>
                            <td class="p-2">${t.t}</td>
                            <td class="p-2 font-bold text-emerald-700">${t.pts}</td>
                            <td class="p-2">${t.nrr}</td>
                        </tr>
                    `;
                });

                container.innerHTML += `
                    <div class="bg-white rounded-lg shadow-md overflow-hidden mb-4">
                        <div class="bg-emerald-700 text-white p-3 font-bold">${group}</div>
                        <table class="w-full text-sm">
                            <tr class="bg-gray-100 border-b text-center text-xs text-gray-600">
                                <th class="p-2 text-left">Team</th>
                                <th class="p-2">P</th>
                                <th class="p-2">W</th>
                                <th class="p-2">L</th>
                                <th class="p-2">T</th>
                                <th class="p-2">Pts</th>
                                <th class="p-2">NRR</th>
                            </tr>
                            ${rows}
                        </table>
                    </div>
                `;
            });
        }

        function checkRecipientUser() {
            let db = getDB();
            let inputVal = document.getElementById("admin-send-userid").value.trim().toLowerCase();
            let statusSpan = document.getElementById("recipient-status");

            if (!inputVal) {
                statusSpan.innerText = "";
                return;
            }

            let foundWallet = null;
            let foundPhone = null;

            if (db.userIDs[inputVal]) {
                foundWallet = db.userIDs[inputVal].wallet;
                foundPhone = db.userIDs[inputVal].phone;
            } else {
                for (let ph in db.users) {
                    if (ph === inputVal) {
                        foundWallet = db.users[ph].wallet;
                        foundPhone = ph;
                        break;
                    }
                }
            }

            if (foundWallet !== null) {
                statusSpan.className = "text-xs font-semibold mt-1 block text-emerald-600";
                statusSpan.innerText = `✅ User found! Phone: ${foundPhone} | Current Wallet: ₹${foundWallet}`;
            } else {
                statusSpan.className = "text-xs font-semibold mt-1 block text-blue-600";
                statusSpan.innerText = `ℹ️ ID not logged in yet. Money will be saved automatically!`;
            }
        }

        function adminSendMoney() {
            let db = getDB();
            let now = new Date().getTime();
            let user = db.users[currentUserPhone];
            let userSubActive = user && user.subscription && user.subscription.activeUntil > now;

            if (currentUserPhone !== "9569981484" && !userSubActive) {
                alert("Access Denied! Aapke number par admin permissions nahi hain.");
                return;
            }

            let inputVal = document.getElementById("admin-send-userid").value.trim().toLowerCase();
            let amount = parseFloat(document.getElementById("admin-send-amount").value);

            if (!inputVal || isNaN(amount) || amount <= 0) {
                alert("Please enter a valid Unique ID / Mobile and amount.");
                return;
            }

            if (inputVal.length === 5) {
                if (!db.userIDs[inputVal]) {
                    db.userIDs[inputVal] = { phone: "Pending Login", wallet: 0 };
                }
                db.userIDs[inputVal].wallet += amount;
                
                let linkedPhone = db.userIDs[inputVal].phone;
                if (linkedPhone && db.users[linkedPhone]) {
                    db.users[linkedPhone].wallet = db.userIDs[inputVal].wallet;
                }
            } else {
                if (!db.users[inputVal]) {
                    db.users[inputVal] = { phone: inputVal, name: "User", userid: inputVal, wallet: 0 };
                }
                db.users[inputVal].wallet += amount;
            }

            saveDB(db);
            alert(`Successfully sent ₹${amount}!`);
            document.getElementById("admin-send-userid").value = "";
            document.getElementById("admin-send-amount").value = "";
            document.getElementById("recipient-status").innerText = "";
            
            if(currentUserPhone) initDashboard();
        }
    </script>
</body>
</html>
