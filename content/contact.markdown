---
title: "Contact Holy Bone! Productions"
draft: false
---

For any inquiries, send an email to:

<button id="contact">Click to reveal email</button>
<script>
function rot10(str) {
    return Array.from(str).map((c) => String.fromCharCode(c.charCodeAt(0) + 10)).join('');
}

function derot10(str) {
    return Array.from(str).map((c) => String.fromCharCode(c.charCodeAt(0) - 10)).join('');
}

const el = document.getElementById('contact');

el.addEventListener('click', (e) => {
    e.preventDefault();

    const replaceEl = document.createElement('span');
    replaceEl.innerText = derot10("sx~ox}s~\u00838\u0084o|y8?B?Jqwksv8myw");

    el.parentNode.insertBefore(replaceEl, el);
    el.parentNode.removeChild(el);
});
</script>
