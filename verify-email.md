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
 
       const app = initializeApp(firebaseConfig);
       const auth = getAuth(app);
 
       const params = new URLSearchParams(window.location.search);
       const mode = params.get("mode");
       const oobCode = params.get("oobCode");
 
       if (mode === "verifyEmail" && oobCode) {
         applyActionCode(auth, oobCode)
           .then(() => {
             window.location.href = "boomboom://verified";
           })
           .catch(err => {
             console.error(err);
             document.getElementById("message").innerHTML = "<h2>Verification failed</h2><p>" + err.message + "</p>";
           });
       } else {
         document.getElementById("message").innerHTML = "<h2>Invalid link</h2>";
       }
     </script>
   </head>
   <body>
  <p>Verifying...</p>
  <p>Please return to the app to continue.</p>
</body>
</html>
