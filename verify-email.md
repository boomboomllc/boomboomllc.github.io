---
layout: default
title: Verifying Email...
---

<html>
<head>
  <title>Verifying Email...</title>
  <script src="https://www.gstatic.com/firebasejs/10.0.0/firebase-app.js"></script>
  <script src="https://www.gstatic.com/firebasejs/10.0.0/firebase-auth.js"></script>
  <script>
    const firebaseConfig = {
      apiKey: "AIzaSyA-H5mHX6UWyzjsJAnNl2rH2SQIzlRUnWk",
      authDomain: "boomboom-9621f.firebaseapp.com"
    };
    firebase.initializeApp(firebaseConfig);
    
    window.onload = async () => {
      document.body.innerHTML = "<p>Verifying your email...</p>";
      const params = new URLSearchParams(window.location.search);
      const oobCode = params.get("oobCode");

      if (oobCode) {
        try {
          await firebase.auth().applyActionCode(oobCode);
          document.body.innerHTML = "<h2>Success</h2><p>Your email has been verified. Please return to the app.</p>";
        } catch (error) {
          document.body.innerHTML = "<h2>Verification Failed</h2><p>Something went wrong. Please contact support.</p>";
        }
      } else {
        document.body.innerHTML = "<h2>Invalid Link</h2><p>No verification code found. Please check your email link.</p>";
      }
    };
  </script>
</head>
<body>
  <p>Loading...</p>
</body>
</html>




