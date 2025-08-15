---
layout: modern
title: "Submit a Post"
permalink: /submit/
---
{% raw %}

<h2>Share your thoughts</h2>
<p>Write a blog post below and submit it to appear on Royi2.</p>

<form id="guest-post-form" style="display: flex; flex-direction: column; gap: 1rem; max-width: 600px;">
  <input type="text" name="title" placeholder="Post title" required style="padding: 0.5rem; font-size: 1rem;">
  <textarea name="body" placeholder="Write your post here..." required rows="8" style="padding: 0.5rem; font-size: 1rem;"></textarea>
  <button type="submit" style="padding: 0.6rem 1rem; background-color: #222; color: #fff; border: none; font-size: 1rem; cursor: pointer;">
    Submit Post
  </button>
</form>

<p id="response-message" style="margin-top: 1rem;"></p>

<script>
  document.getElementById("guest-post-form").addEventListener("submit", async function(e) {
    e.preventDefault();
    const form = e.target;
    const title = form.title.value.trim();
    const body = form.body.value.trim();

    if (!title || !body) {
      document.getElementById("response-message").textContent = "Please fill out both fields.";
      return;
    }

    try {
      const response = await fetch("https://silver-boba-68fd60.netlify.app/.netlify/functions/submit-post", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ title, body })
      });

      if (!response.ok) throw new Error("Network response was not ok");

      const result = await response.json();
      document.getElementById("response-message").textContent = result.message || "Post submitted!";
    } catch (error) {
      document.getElementById("response-message").textContent = "Submission failed. Please try again.";
      console.error("Submission error:", error);
    }
  });
</script>
{% endraw %}

