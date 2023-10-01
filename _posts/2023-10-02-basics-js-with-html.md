---
toc: true
comments: true
layout: post
title: Basics of JS with HTML
description: This is for the Web Programming to work
type: hacks
courses: { compsci: {week: 6} }
---

<head>
  <div id="divContainerIDbutton">
      <h1 id="h1ElementIDbutton">Varnika's Mystery Button</h1>
      <p id= "Unswitched">Unswitched</p>
  </div>
  <!-- the ID must be specified on the elements -->
<button id="buttonID">DONT PUSH THIS BUTTON</button>
<br>
<a href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"> Don't click it... </a>
<br>
<a href="https://en.wikipedia.org/wiki/Rickrolling"> Don't do it... </a>
<head>
  <div>
      <p> I told you not to do it...</p>
  </div>
</head>

<script>
  const link1 = document.querySelector('a[href="https://www.youtube.com/watch?v=dQw4w9WgXcQ"]');
  const link2 = document.querySelector('a[href="https://en.wikipedia.org/wiki/Rickrolling"]');
  const button = document.getElementById('buttonID');

  button.addEventListener('click', function () {1
    if (link1.href === 'https://www.youtube.com/watch?v=dQw4w9WgXcQ') {
      link1.href = 'https://en.wikipedia.org/wiki/Rickrolling';
      link2.href = 'https://www.youtube.com/watch?v=dQw4w9WgXcQ';
      document.getElementById("Unswitched").innerHTML = "Switched"
    } else {
      link1.href = 'https://www.youtube.com/watch?v=dQw4w9WgXcQ';
      link2.href = 'https://en.wikipedia.org/wiki/Rickrolling';
      document.getElementById("Unswitched").innerHTML = "Switched"
    }
  });
</script>