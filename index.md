---
layout: page
title: 🏡 Home
description: >-
  "Information about EECS 245: Mathematics for Machine Learning in Fall 2025 at the University of Michigan."
nav_order: 1
---

<!-- Embed MathJax for LaTeX rendering -->
<script>
window.MathJax = {
  tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}
};
</script>
<script src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js" async></script>

{: .red }
**This is the course website for a previous iteration of the course. If you’re looking for the most recent course website, look at [eecs245.org](https://eecs245.org).** Links to lecture recordings below will still work, but other links may not.

# Mathematics for Machine Learning 🧠
{: .no_toc }
{: .mb-2 }
EECS 245, Winter 2026 at the <b><span style="background-color: #FFCB05; color: #00274C">University of Michigan</span></b>
{: .no_toc }
{: .fs-6 .fw-300 .mb-2 }

{% for staffer in site.staffersnobio %}
{{ staffer }}
{% endfor %}

{% for module in site.modules %}
{{ module }}
{% endfor %}

<script>
(function() {
  const jumpLink = document.querySelector('[data-current-week-link]');
  if (!jumpLink) {
    return;
  }

  const modules = Array.from(document.querySelectorAll('.module'));
  if (!modules.length) {
    return;
  }

  const parseDate = (value) => {
    if (!value) {
      return null;
    }
    const parsed = new Date(value + 'T00:00:00');
    if (Number.isNaN(parsed.getTime())) {
      return null;
    }
    return parsed;
  };

  const moduleData = modules
    .map((moduleEl) => {
      const start = parseDate(moduleEl.dataset.weekStart);
      const end = parseDate(moduleEl.dataset.weekEnd);
      const header = moduleEl.querySelector('.module-header');
      if (!start || !end || !header || !header.id) {
        return null;
      }
      return { start, end, header };
    })
    .filter(Boolean);

  if (!moduleData.length) {
    return;
  }

  moduleData.sort((a, b) => a.start - b.start);

  const today = new Date();
  const todayMidnight = new Date(today.getFullYear(), today.getMonth(), today.getDate());
  let target = moduleData.find((module) => (
    todayMidnight >= module.start && todayMidnight <= module.end
  ));

  if (!target) {
    if (todayMidnight < moduleData[0].start) {
      target = moduleData[0];
    } else {
      for (let i = moduleData.length - 1; i >= 0; i -= 1) {
        if (todayMidnight > moduleData[i].end) {
          target = moduleData[i];
          break;
        }
      }
    }
  }

  if (target) {
    jumpLink.setAttribute('href', '#' + target.header.id);
  }
})();
</script>
