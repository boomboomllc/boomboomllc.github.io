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
      const statusMessage = document.getElementById("status-message");
      statusMessage.innerHTML = "<p>Loading...</p>"; // Show "Loading..." initially
      
      // Force the UI to repaint before continuing with the logic
      await new Promise(resolve => setTimeout(resolve, 0));

      const params = new URLSearchParams(window.location.search);
      const oobCode = params.get("oobCode");

      if (!oobCode) {
        // Immediately show the invalid link message if no oobCode
        statusMessage.innerHTML = "<h2>Invalid Link</h2><p>No verification code found. Please check your email link.</p>";
        return;
      }

      try {
        // Attempt to verify the code
        await firebase.auth().applyActionCode(oobCode);
        statusMessage.innerHTML = "<h2>Success</h2><p>Your email has been verified. Please return to the app.</p>";
      } catch (error) {
        // If an error occurs, show an error message
        console.error("Verification error:", error); // For debugging
        statusMessage.innerHTML = "<h2>Error</h2><p>There was an error verifying your email. Please try again or contact support.</p>";
      }
    };
  </script>
</head>
<body>
  <div id="status-message"><p>Loading...</p></div>
</body>
</html>
