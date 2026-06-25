---
layout: page
title: Map
permalink: /map/
weight: 5
---

# **Academic Map**

Places where I've studied and done research. Scroll to zoom, drag to pan.

<div id="academic-map" style="height: 520px; width: 100%; border-radius: 8px; margin-top: 1rem; background: #eef2f5; position: relative; overflow: hidden;"></div>

<p class="text-muted" style="margin-top: .75rem;">
  <span style="color:#2a7de1;">&#9679;</span> Research &nbsp;
  <span style="color:#e07a2a;">&#9679;</span> Education
</p>

<script src="https://cdn.jsdelivr.net/npm/d3@7"></script>
<script src="https://cdn.jsdelivr.net/npm/topojson-client@3"></script>
<script>
window.addEventListener('load', function () {
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

  var el = document.getElementById('academic-map');

  function draw() {
    el.innerHTML = '';  // clear any previous render
    var width  = el.clientWidth  || 700;
    var height = el.clientHeight || 520;

    var svg = d3.select(el).append('svg')
      .attr('width', width)
      .attr('height', height)
      .style('display', 'block');

    var g = svg.append('g');

    function colorFor(type) {
      if (type === 'research') return '#2a7de1';
      if (type === 'education') return '#e07a2a';
      return '#6c757d';
    }

    var meanLng = places.length ? d3.mean(places, function(d){return d.lng;}) : 12;
    var meanLat = places.length ? d3.mean(places, function(d){return d.lat;}) : 50;

    var projection = d3.geoMercator()
      .center([meanLng, meanLat])
      .scale(width * 0.9)
      .translate([width / 2, height / 2]);

    var path = d3.geoPath().projection(projection);
    var worldUrl = 'https://cdn.jsdelivr.net/npm/world-atlas@2/countries-110m.json';

    d3.json(worldUrl).then(function (world) {
      var countries = topojson.feature(world, world.objects.countries);

      g.selectAll('path.country')
        .data(countries.features)
        .enter().append('path')
          .attr('class', 'country')
          .attr('d', path)
          .attr('fill', '#d8dee4')
          .attr('stroke', '#fff')
          .attr('stroke-width', 0.5);

      var pins = g.selectAll('circle.pin')
        .data(places)
        .enter().append('circle')
          .attr('class', 'pin')
          .attr('cx', function(d){ return projection([d.lng, d.lat])[0]; })
          .attr('cy', function(d){ return projection([d.lng, d.lat])[1]; })
          .attr('r', 6)
          .attr('fill', function(d){ return colorFor(d.type); })
          .attr('stroke', '#fff')
          .attr('stroke-width', 1.5)
          .style('cursor', 'pointer');

      var tip = d3.select(el).append('div')
        .style('position', 'absolute')
        .style('pointer-events', 'none')
        .style('background', 'rgba(0,0,0,0.8)')
        .style('color', '#fff')
        .style('padding', '6px 9px')
        .style('border-radius', '5px')
        .style('font-size', '13px')
        .style('opacity', 0);

      pins.on('mouseover', function (event, d) {
          var txt = '<strong>' + d.name + '</strong>';
          if (d.role)  txt += '<br>' + d.role;
          if (d.years) txt += '<br>' + d.years;
          tip.html(txt).style('opacity', 1);
        })
        .on('mousemove', function (event) {
          var r = el.getBoundingClientRect();
          tip.style('left', (event.clientX - r.left + 12) + 'px')
             .style('top',  (event.clientY - r.top  + 12) + 'px');
        })
        .on('mouseout', function () { tip.style('opacity', 0); })
        .on('click', function (event, d) { if (d.url) window.open(d.url, '_blank'); });

      var zoom = d3.zoom()
        .scaleExtent([1, 12])
        .on('zoom', function (event) {
          g.attr('transform', event.transform);
          g.selectAll('path.country').attr('stroke-width', 0.5 / event.transform.k);
          g.selectAll('circle.pin')
            .attr('r', 6 / event.transform.k)
            .attr('stroke-width', 1.5 / event.transform.k);
        });

      svg.call(zoom);
    });
  }

  // Draw once layout is settled, and redraw on resize.
  setTimeout(draw, 100);
  var rt;
  window.addEventListener('resize', function () {
    clearTimeout(rt); rt = setTimeout(draw, 200);
  });
});
</script>
