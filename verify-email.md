---
layout: default
title: Verifying Email...
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Email Verification</title>
</head>
<body>
    <h1>Email Verification</h1>
    <p id="status">Verifying your email...</p>

    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-auth.js"></script>

    <script>
        // Initialize Firebase with your Firebase config
        const firebaseConfig = {
         apiKey: "AIzaSyA-H5mHX6UWyzjsJAnNl2rH2SQIzlRUnWk",
         authDomain: "boomboom-9621f.firebaseapp.com",
         projectId: "boomboom-9621f",
         storageBucket: "boomboom-9621f.appspot.com",
         messagingSenderId: "396477438586",
         appId: "1:396477438586:web:4d7e266b0d88fedaf839c3"
     };

        firebase.initializeApp(firebaseConfig);

        // Extract the action code from the URL (e.g., ?oobCode=someCode)
        const urlParams = new URLSearchParams(window.location.search);
        const actionCode = urlParams.get('oobCode');

        if (!actionCode) {
            document.getElementById('status').innerText = "Verification code is missing.";
            return;
        }

        // Check the action code with Firebase
        firebase.auth().checkActionCode(actionCode)
            .then(function(info) {
                // If the code is valid, apply the action code (verify email)
                return firebase.auth().applyActionCode(actionCode);
            })
            .then(function() {
                // Successfully verified email
                document.getElementById('status').innerText = "Email verified successfully!";
                setTimeout(function() {
                    window.location.href = '/success.html';  // Redirect to success page
                }, 2000);
            })
            .catch(function(error) {
                // Handle invalid or expired code
                document.getElementById('status').innerText = "This verification link is expired or invalid.";
                setTimeout(function() {
                    window.location.href = '/failure.html';  // Redirect to failure page
                }, 2000);
            });
    </script>
</body>
</html>


