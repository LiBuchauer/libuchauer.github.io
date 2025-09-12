---
layout: page
title: Publications
order: 5
---

{% for pub in site.data.publist %}

  **{{ pub.title }}** <br />
  <small>
  {{ pub.authors }}<br />
  </small>
  {{ pub.journal }} ({{ pub.year }})
{% if pub.links.arxiv %}[<i class="ai ai-arxiv"></i>]({{ pub.links.arxiv }}){% endif %}{% if pub.links.doi %}[<i class="ai ai-doi"></i>]({{ pub.links.doi }}){% endif %}{% if pub.links.pdf %}[<i class="ai ai-open-access"></i>]({{ pub.links.pdf }}){% endif %}{% if pub.links.github %}[<i class="fa fa-github"></i>]({{ pub.links.github }}){% endif %}
{% if pub.media %}
<small>
{{ pub.media }}
</small>
{% endif %}
<br>
{% endfor %}

\* equal first author contribution  
\*\* equal last author contribution
