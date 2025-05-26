---
layout: default
title: Authenticating..
permalink: /auth/action/
---

<div id="message">Redirecting...</div>

<script>
  const params = new URLSearchParams(window.location.search);
  const mode = params.get('mode');
  const oobCode = params.get('oobCode');

  const app = initializeApp(firebaseConfig);
  const auth = getAuth(app);

  const params = new URLSearchParams(window.location.search);
  const mode = params.get('mode');
  const oobCode = params.get('oobCode');
  const continueUrl = params.get('continueUrl');
  const lang = params.get('lang') || 'en';

  if (!mode || !oobCode) {
    document.body.innerHTML = '<h2>Invalid action URL.</h2>';
  } else {
    switch (mode) {
      case 'resetPassword':
        // Redirect to your reset-password page with all parameters
        window.location.href = `/reset-password/?oobCode=${encodeURIComponent(oobCode)}&mode=${encodeURIComponent(mode)}&continueUrl=${encodeURIComponent(continueUrl || '')}&lang=${encodeURIComponent(lang)}`;
        break;
      case 'verifyEmail':
        // Redirect to your verify-email page with all parameters
        window.location.href = `/verify-email/?oobCode=${encodeURIComponent(oobCode)}&mode=${encodeURIComponent(mode)}&continueUrl=${encodeURIComponent(continueUrl || '')}&lang=${encodeURIComponent(lang)}`;
        break;
      case 'recoverEmail':
        // Handle recoverEmail mode if needed, else redirect to home
        window.location.href = '/';
        break;
      default:
        // Unknown mode, redirect home
        window.location.href = '/';
        break;
    }
  }
</script>
