---
layout: home
title: "My Foolproof Homepage"
---

{% raw %}
<style>
  body {
    font-family: sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    background-color: #f0f2f5;
    color: #333;
  }
  .container {
    background-color: white;
    padding: 2em 3em;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    text-align: center;
    max-width: 600px;
    width: 90%;
  }
  h1 {
    color: #2c3e50;
    margin-bottom: 0.5em;
  }
  p {
    font-size: 1.1em;
    line-height: 1.6;
    margin-bottom: 1.5em;
  }
  .button {
    display: inline-block;
    padding: 10px 20px;
    background-color: #3498db;
    color: white;
    text-decoration: none;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  .button:hover {
    background-color: #2980b9;
  }
</style>

<div class="container">
  <h1>Hello, Jekyll!</h1>
  <p>
    This is a simple, foolproof `index.md` page. 
    It contains no complex Liquid logic to avoid common syntax errors.
    If this builds successfully, the problem is likely in more complex Liquid code 
    or specific theme interactions elsewhere.
  </p>
  <a href="#" class="button">Learn More</a>
</div>
{% endraw %}
