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
      const params = new URLSearchParams(window.location.search);
      const oobCode = params.get("oobCode");
     if (oobCode) {
        try {
          await firebase.auth().applyActionCode(oobCode);
          document.body.innerHTML = "<h2>Email verified!</h2><p>You can now return to the app.</p>";
        } catch (error) {
          document.body.innerHTML = `<h2>Error</h2><p>${error.message}</p>`;
        }
      } else {
        document.body.innerHTML = "<h2>Invalid verification link.</h2>";
      }
    };
  </script>
</head>
<body>
  <p>Email Verified!\n\nPlease return to the app to continue.</p>
</body>
</html>


