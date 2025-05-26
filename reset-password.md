---
layout: default
title: Reset Password
---

<h2>Reset Your Password</h2>

<div id="reset-password-form" style="display: none;">
  <input type="password" id="new-password" placeholder="New password" />
  <button onclick="submitNewPassword()">Reset Password</button>
</div>

<p id="message">Loading...</p>

<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-app.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.0/firebase-auth.js"></script>
<script>
const firebaseConfig = {
  apiKey: "AIzaSyA-H5mHX6UWyzjsJAnNl2rH2SQIzlRUnWk",
  authDomain: "boomboom-9621f.firebaseapp.com",
  projectId: "boomboom-9621f",
  storageBucket: "boomboom-9621f.appspot.com",
  messagingSenderId: "396477438586",
  appId: "1:396477438586:web:4d7e266b0d88fedaf839c3"
};

firebase.initializeApp(firebaseConfig);

const params = new URLSearchParams(window.location.search);
const oobCode = params.get("oobCode");

if (!oobCode) {
  document.getElementById('message').innerText = 'Missing reset code.';
} else {
  firebase.auth().verifyPasswordResetCode(oobCode)
    .then(() => {
      document.getElementById('reset-password-form').style.display = 'block';
      document.getElementById('message').innerText = '';
    })
    .catch(() => {
      document.getElementById('message').innerText = 'Invalid or expired password reset link.';
    });
}

function submitNewPassword() {
  const newPassword = document.getElementById('new-password').value;
  firebase.auth().confirmPasswordReset(oobCode, newPassword)
    .then(() => {
      document.getElementById('message').innerText = 'Password has been reset.';
      document.getElementById('reset-password-form').style.display = 'none';
    })
    .catch(() => {
      document.getElementById('message').innerText = 'Error resetting password.';
    });
}
</script>
