---
layout: default
title: Verifying Email...
---

 <html>
   <head>
     <meta charset="UTF-8">
     <title>Verifying Email...</title>
     <script type="module">
       import { initializeApp } from "https://www.gstatic.com/firebasejs/10.10.0/firebase-app.js";
       import { getAuth, applyActionCode } from "https://www.gstatic.com/firebasejs/10.10.0/firebase-auth.js";
 
       const firebaseConfig = {
         apiKey: "AIzaSyA-H5mHX6UWyzjsJAnNl2rH2SQIzlRUnWk",
         authDomain: "boomboom-9621f.firebaseapp.com",
         projectId: "boomboom-9621f",
         storageBucket: "boomboom-9621f.appspot.com",
         messagingSenderId: "396477438586",
         appId: "1:396477438586:web:4d7e266b0d88fedaf839c3"
     };
 
       firebase.initializeApp(firebaseConfig);

        // Get the verification code from the URL
        const urlParams = new URLSearchParams(window.location.search);
        const actionCode = urlParams.get('oobCode');

        if (!actionCode) {
            document.getElementById('status').innerText = "Verification code is missing.";
            return;
        }

        // Check the verification code (action code) with Firebase
        firebase.auth().checkActionCode(actionCode)
            .then(function(info) {
                // If the action code is valid, verify the email
                return firebase.auth().applyActionCode(actionCode);
            })
            .then(function() {
                // Successfully verified the email
                document.getElementById('status').innerText = "Email verified successfully!";
                setTimeout(() => {
                    window.location.href = '/success.html'; // Redirect to success page
                }, 2000);
            })
            .catch(function(error) {
                // Handle errors (invalid/expired link)
                document.getElementById('status').innerText = "This verification link has expired or is invalid.";
                setTimeout(() => {
                    window.location.href = '/failure.html'; // Redirect to failure page
                }, 2000);
            });
    </script>
</body>
</html>


