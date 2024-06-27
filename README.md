
<html>
<head>
	<title>Hirana Miner</title>
	<style>
		/* Global Styles */
		* {
			box-sizing: border-box;
			margin: 0;
			padding: 0;
		}
		body {
			font-family: Arial, sans-serif;
			background-image: linear-gradient(to bottom, #3498db, #2980b9); /* blue gradient */
			background-size: 100% 300px;
			background-position: 0% 100%;
			height: 100vh;
			margin: 0;
		}
		
		/* Container Styles */
		.container {
			width: 80%;
			margin: 40px auto;
			padding: 20px;
			background-color: #fff;
			border: 1px solid #ddd;
			border-radius: 10px;
			box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
		}
		
		/* Header Styles */
		.header {
			background-color: #3498db; /* blue */
			color: #fff;
			padding: 10px;
			text-align: center;
			border-radius: 10px 10px 0 0;
		}
		
		/* Account Styles */
		.account {
			padding: 20px;
		}
		.account h2 {
			margin-top: 0;
			color: #666; /* dark gray */
		}
		.balance {
			font-size: 24px;
			font-weight: bold;
			margin-bottom: 20px;
			color: #2ecc71; /* green */
		}
		.hashrate {
			font-size: 18px;
			margin-bottom: 10px;
			color: #9b59b6; /* purple */
		}
		
		/* Button Styles */
		.button {
			background-color: #4CAF50; /* green */
			color: #fff;
			padding: 10px 20px;
			border: none;
			border-radius: 5px;
			cursor: pointer;
		}
		.button:hover {
			background-color: #3e8e41; /* darker green */
		}
		
		/* Upgrade Styles */
		.upgrade {
			margin-top: 20px;
		}
		.upgrade-button {
			background-color: #337ab7; /* blue */
			color: #fff;
			padding: 10px 20px;
			border: none;
			border-radius: 5px;
			cursor: pointer;
		}
		.upgrade-button:hover {
			background-color: #23527c; /* darker blue */
		}
		
		/* Notification Styles */
		.notification {
			background-color: #f0f0f0;
			padding: 10px;
			border: 1px solid #ccc;
			border-radius: 5px;
			margin-bottom: 20px;
		}
		
		/* Leaderboard Styles */
		.leaderboard {
			padding: 20px;
		}
		.leaderboard h2 {
			margin-top: 0;
			color: #666; /* dark gray */
		}
		.leaderboard-table {
			border-collapse: collapse;
			width: 100%;
		}
		.leaderboard-table th, .leaderboard-table td {
			border: 1px solid #ddd;
			padding: 10px;
			text-align: left;
		}
		.leaderboard-table th {
			background-color: #f0f0f0;
		}
		
		/* Responsive Design */
		@media (max-width: 768px) {
			.container {
				width: 90%;
			}
		}
	</style>
</head>
<body>
	<div class="container">
		<div class="header">
			<h1>Hirana Miner</h1>
		</div>
		<div class="account">
			<h2>Account</h2>
			<p>Welcome, <span id="username-display"></span>!</p>
			<p>Your balance: <span id="balance">0</span> </p>
			<p>Your hashrate: <span id="hashrate">1</span> </p>
			<button class="button" id="mine-button">Start Mining!</button>
			
			<div class="upgrade">
				<h2>Upgrades</h2>
				<p>GPU Upgrade: +0.0001 H/s (cost: 1 HRN)</p>
				<button class="upgrade-button" id="gpu-upgrade">Buy</button>
				<p>ASICUpgrade: +0.0005 H/s (cost: 2.5 HRN)</p>
				<button class="upgrade-button" id="asic-upgrade">Buy</button>
				<p>FPGA Upgrade: +0.0003 H/s (cost: 1.8 HRN)</p>
				<button class="upgrade-button" id="fpga-upgrade">Buy</button>
				<p>Quantum Upgrade: +0.001 H/s (cost: 5 HRN)</p>
				<button class="upgrade-button" id="quantum-upgrade">Buy</button>
			</div>
			
			<div id="notifications"></div>
<h2>Login/Register</h2>
			<input type="text" id="username-input" placeholder="Username">
			<input type="password" id="password-input" placeholder="Password">
			<button class="button" id="login-button">Login</button>
			<button class="button" id="register-button">Register</button>
		</div>
		
		<!-- Leaderboard Tab -->
		<div class="leaderboard">
			<h2>Leaderboards</h2>
			<table class="leaderboard-table">
				<thead>
					<tr>
						<th>Rank</th>
						<th>Username</th>
						<th>Balance</th>
						<th>Hashrate</th>
					</tr>
				</thead>
				<tbody id="leaderboard-table-body">
					<!-- Leaderboard data will be displayed here -->
				</tbody>
			</table>
		</div>
		
	<script>
			var accounts = {};
			var currentUser = null;
			
			document.getElementById("login-button").addEventListener("click", function() {
				var username = document.getElementById("username-input").value;
				var password = document.getElementById("password-input").value;
				if (accounts[username]&& accounts[username].password === password) {
					currentUser = accounts[username];
					document.getElementById("username-display").innerHTML = username;
					document.getElementById("balance").innerHTML = currentUser.balance + " Hirana";
					document.getElementById("hashrate").innerHTML = currentUser.hashrate + " H/s";
				} else {
					alert("Invalid username or password");
				}
			});
			
			document.getElementById("register-button").addEventListener("click", function() {
				var username = document.getElementById("username-input").value;
				var password = document.getElementById("password-input").value;
				if (!accounts[username]) {
					accounts[username] = {
						balance: 0,
						hashrate: 0.0001,
						password:password
					};
currentUser = accounts[username];
					document.getElementById("username-display").innerHTML = username;
					document.getElementById("balance").innerHTML = currentUser.balance + " Hirana";
					document.getElementById("hashrate").innerHTML = currentUser.hashrate + " H/s";
					
					// Save progress automatically
					localStorage.setItem("accounts", JSON.stringify(accounts));
				} else {
					alert("Username already exists");
				}
			});
			
			// Load saved progress
			if (localStorage.getItem("accounts")) {
				accounts = JSON.parse(localStorage.getItem("accounts"));
			}
			
			var username = "Player";
			var balance = 0;
			var hashrate = 0.0001;
			var mining = false;
			var notifications = [];
			
			if (currentUser) {
				username = currentUser.username;
				balance = currentUser.balance;
				hashrate = currentUser.hashrate;
			}
			
			document.getElementById("username-display").innerHTML = username;
			document.getElementById("balance").innerHTML = balance + " Hirana";
			document.getElementById("hashrate").innerHTML = hashrate + " H/s";
			
			document.getElementById("mine-button").addEventListener("click", function() {
				if (!mining) {
					mining = true;
					document.getElementById("mine-button").innerHTML = "Stop Mining!";
					mineHirana();
				} else {
					mining = false;
					document.getElementById("mine-button").innerHTML = "Start Mining!";
					clearTimeout(mineHiranaTimeout);
				}
			});
			
			var mineHiranaTimeout;
			function mineHirana() {
				balance += hashrate;
				document.getElementById("balance").innerHTML = balance + " Hirana";
				mineHiranaTimeout = setTimeout(mineHirana, 1000);
				
				// Save progress automatically
				localStorage.setItem("accounts", JSON.stringify(accounts));
			}
			
			document.getElementById("gpu-upgrade").addEventListener("click", function() {
				if (balance >= 1) {
					balance -= 1;
					hashrate += 0.0001;
					document.getElementById("balance").innerHTML = balance + " Hirana";
					document.getElementById("hashrate").innerHTML= hashrate + " H/s";
					
					// Save progress automatically
					localStorage.setItem("accounts", JSON.stringify(accounts));
					
					// Add notification
					notifications.push("GPU Upgrade purchased!");
					updateNotifications();
				}
			});
			
			document.getElementById("asic-upgrade").addEventListener("click", function() {
				if (balance >= 2.5) {
					balance -= 2.5;
					hashrate += 0.0005;
					document.getElementById("balance").innerHTML = balance + " Hirana";
					document.getElementById("hashrate").innerHTML = hashrate + " H/s";
					
					// Save progress automatically
					localStorage.setItem("accounts", JSON.stringify(accounts));
					
					// Add notification
					notifications.push("ASIC Upgrade purchased!");
					updateNotifications();
				}
			});

            document.getElementById("fpga-upgrade").addEventListener("click", function() {
				if (balance >= 1.8) {
					balance -= 1.8;
					hashrate += 0.0003;
					document.getElementById("balance").innerHTML = balance + " Hirana";
					document.getElementById("hashrate").innerHTML = hashrate + " H/s";
					
					// Save progress automatically
				localStorage.setItem("accounts", JSON.stringify(accounts));
					
					// Add notification
					notifications.push("FPGA Upgrade purchased!");
					updateNotifications();
				}
			});
			
			document.getElementById("quantum-upgrade").addEventListener("click", function() {
				if (balance >= 5) {
					balance -= 5;
					hashrate += 0.001;
					document.getElementById("balance").innerHTML = balance + " Hirana";
					document.getElementById("hashrate").innerHTML = hashrate + " H/s";
					
					// Save progress automatically
					localStorage.setItem("accounts", JSON.stringify(accounts));
					
					// Add notification
					notifications.push("Quantum Upgrade purchased!");
					updateNotifications();
				}
			});
			
			function updateNotifications() {
				var notificationHTML = "";
				for (var i = 0; i < notifications.length; i++) {
					notificationHTML += "<div class='notification'>" + notifications[i] + "</div>";
				}
				document.getElementById("notifications").innerHTML = notificationHTML;
			}
			
			// Leaderboard functionality
			function updateLeaderboard() {
				var leaderboardHTML = "";
				var sortedAccounts = Object.values(accounts).sort(function(a, b) {
					return b.balance - a.balance;
				});
				for (var i = 0; i < sortedAccounts.length; i++) {
					leaderboardHTML += "<tr><td>" + (i + 1) + "</td><td>" + sortedAccounts[i].username + "</td><td>" + sortedAccounts[i].balance + " Hirana</td><td>" + sortedAccounts[i].hashrate + " H/s</td></tr>";
				}
				document.getElementById("leaderboard-table-body").innerHTML = leaderboardHTML;
			}
			
			// Update leaderboard every 10 seconds
			setInterval(updateLeaderboard, 10000);
		</script>
	</div>
</body>
</html>
