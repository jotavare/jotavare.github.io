---
title: Home
layout: home
nav_order: 1
---

# **WELCOME**

Hey there! This project initially served as a testing ground for GitHub Pages and Jekyll. However, it evolved into something more significant. I realized the potential to transform the documentation I already had scattered across various GitHub repositories into a unified, easily searchable website format. Thus, this platform serves as a comprehensive documentation hub, packed with resources, guides, cheat sheets, and more, all tailored for personal use.

My aim is to document everything essential to my journey - from my experiences at 42 school to my personal hobbies and work-related insights. Your suggestions are always welcome, and any contributions you make are highly valued.

I hope this platform can help you on your journey, sparing you the struggles I faced in scouring for information. Happy coding!

<button class="btn js-toggle-light-mode">Don't click here!</button>

<script>
const toggleLightMode = document.querySelector('.js-toggle-light-mode');

jtd.addEvent(toggleLightMode, 'click', function(){
  if (jtd.getTheme() === 'light') {
    jtd.setTheme('dark');
    toggleLightMode.textContent = 'Don\'t click here!';
  } else {
    jtd.setTheme('light');
    toggleLightMode.textContent = 'Return to the dark side';
  }
});
</script>