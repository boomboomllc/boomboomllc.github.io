---
layout: default
title: Firebase Action
permalink: /auth/action/
---

<script type="module">
  const params = new URLSearchParams(window.location.search);
  const mode = params.get("mode");

  if (mode === "verifyEmail") {
    window.location.href = "/verify-email.html" + window.location.search;
  } else if (mode === "resetPassword") {
    window.location.href = "/reset-password.html" + window.location.search;
  } else {
    document.body.innerHTML = "<h2>Invalid action</h2>";
  }
</script>
