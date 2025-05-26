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

  if (!mode || !oobCode) {
    document.getElementById('message').innerText = 'Invalid request.';
  } else {
    switch (mode) {
      case 'resetPassword':
        window.location.href = `/reset-password?oobCode=${encodeURIComponent(oobCode)}`;
        break;
      case 'verifyEmail':
        window.location.href = `/verify-email?oobCode=${encodeURIComponent(oobCode)}`;
        break;
      default:
        document.getElementById('message').innerText = 'Unsupported action.';
    }
  }
</script>
