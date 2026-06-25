---
layout: page
title: Map
permalink: /map/
weight: 5
---

# **Academic Map**

Places where I've studied and done research.

<!-- Leaflet CSS & JS (free, open-source maps; no API key needed) -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<div id="academic-map" style="height: 70vh; min-height: 420px; width: 100%; border-radius: 8px; margin-top: 1rem;"></div>

<p class="text-muted" style="margin-top: .75rem;">
  <span style="color:#2a7de1;">&#9679;</span> Research &nbsp;
  <span style="color:#e07a2a;">&#9679;</span> Education
</p>

<script>
(function () {
  // Pull place data from the Jekyll data file.
  var places = [
    {% assign place_list = site.data["map-places"] %}
    {% for p in place_list %}
    {
      name: {{ p.name | jsonify }},
      lat: {{ p.lat }},
      lng: {{ p.lng }},
      role: {{ p.role | default: "" | jsonify }},
      years: {{ p.years | default: "" | jsonify }},
      type: {{ p.type | default: "" | jsonify }},
      url: {{ p.url | default: "" | jsonify }}
    }{% unless forloop.last %},{% endunless %}
    {% endfor %}
  ];

  var map = L.map('academic-map');
  L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
  }).addTo(map);

  function colorFor(type) {
    if (type === 'research') return '#2a7de1';
    if (type === 'education') return '#e07a2a';
    return '#6c757d';
  }

  var bounds = [];
  places.forEach(function (p) {
    var marker = L.circleMarker([p.lat, p.lng], {
      radius: 9,
      color: '#fff',
      weight: 2,
      fillColor: colorFor(p.type),
      fillOpacity: 0.95
    }).addTo(map);

    var html = '<strong>' + p.name + '</strong>';
    if (p.role)  html += '<br>' + p.role;
    if (p.years) html += '<br><span style="color:#888;">' + p.years + '</span>';
    if (p.url)   html += '<br><a href="' + p.url + '" target="_blank" rel="noopener">website</a>';
    marker.bindPopup(html);

    bounds.push([p.lat, p.lng]);
  });

  if (bounds.length === 1) {
    map.setView(bounds[0], 6);
  } else if (bounds.length > 1) {
    map.fitBounds(bounds, { padding: [50, 50] });
  } else {
    map.setView([48.2, 16.3], 4);
  }
})();
</script>
