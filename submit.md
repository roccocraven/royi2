---
layout: page
title: Submit a Post
permalink: /submit/
---

{% raw %}
<h1>Submit a Post</h1>

<form id="submitForm">
  <label>Title<br/>
    <input type="text" id="title" required />
  </label>
  <br/><br/>
  <label>Body<br/>
    <textarea id="body" rows="10" required></textarea>
  </label>
  <br/><br/>
  <button type="submit">Publish</button>
</form>

<pre id="result" style="margin-top:1rem;"></pre>

<script>
const endpoint = "' + $NetlifyBase + '/.netlify/functions/submit-post";

document.getElementById("submitForm").addEventListener("submit", async (e) => {
  e.preventDefault();

  const title = document.getElementById("title").value.trim();
  const body  = document.getElementById("body").value.trim();

  const res = await fetch(endpoint, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ title, body })
  });

  const text = await res.text();
  document.getElementById("result").textContent = `Status ${res.status}: ${text}`;
});
</script>
{% endraw %}