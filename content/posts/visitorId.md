---
title: "Show visitor id"
date: 2022-05-24T00:28:40+02:00
summary: "Show visitor Id using fingerprintjs"
---

Visitor Id: <span id="visitor"></span>
<script>
    const fpPromise = import('https://openfpcdn.io/fingerprintjs/v3')
        .then(FingerprintJS => FingerprintJS.load());
    fpPromise
        .then(fp => fp.get())
        .then(result => {
            // This is the visitor identifier:
            const visitorId = result.visitorId
            const visitor = document.getElementById("visitor")
            visitor.innerText = visitorId;
        });
</script>