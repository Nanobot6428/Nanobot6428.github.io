---
title: Services and Price List
permalink: /services/
---

## Prices Starting 1st October 2025:

#### Loyalty Discount - Clean again within 3 months to get up to a 15% discount 
 - Interval and discount applies to cars individually

#### Car Categories:
**Small:** Superminis e.g. Ford Fiesta, VW Polo  
**Medium:** Most cars: hatchbacks, SUVs, small estates, saloons, etc.  
**Large:** Any car with a boot over 600 litres and vans smaller than a Ford Transit Custom  
**Very Large:** Cars with three rows of seats and vans a similar size and larger than a Ford Transit Custom  
Note: Only the passenger area in a van is cleaned, not cargo area.  

<link rel="stylesheet" href="/assets/css/services/services.css" type="text/css">

<h2 style="margin-bottom:1rem;">Car Services</h2>

<!-- Filter Controls -->
<div class="filter-section">
  <strong>Category:</strong>
  <div class="filter-group">
    <button type="button" onclick="filterServices('all', this)" class="filter-btn filter-btn--primary is-active" data-filter="all">All</button>
    <button type="button" onclick="filterServices('exterior', this)" class="filter-btn filter-btn--success">Exterior</button>
    <button type="button" onclick="filterServices('valet', this)" class="filter-btn filter-btn--success">Valet</button>
    <button type="button" onclick="filterServices('mixed', this)" class="filter-btn filter-btn--success">Mixed</button>
    <button type="button" onclick="filterServices('interior', this)" class="filter-btn filter-btn--success">Interior</button>
  </div>
</div>

<div class="filter-section">
  <strong>Exterior Depth:</strong>
  <div class="filter-group">
    <button type="button" onclick="filterExterior('all', this)" class="filter-btn filter-btn--info is-active" data-filter="all">All</button>
    <button type="button" onclick="filterExterior('none', this)" class="filter-btn filter-btn--info">None</button>
    <button type="button" onclick="filterExterior('basic', this)" class="filter-btn filter-btn--info">Basic</button>
    <button type="button" onclick="filterExterior('standard', this)" class="filter-btn filter-btn--info">Standard</button>
    <button type="button" onclick="filterExterior('deep', this)" class="filter-btn filter-btn--info">Deep</button>
  </div>
</div>

<div class="filter-section">
  <strong>Interior Depth:</strong>
  <div class="filter-group">
    <button type="button" onclick="filterInterior('all', this)" class="filter-btn filter-btn--danger is-active" data-filter="all">All</button>
    <button type="button" onclick="filterInterior('none', this)" class="filter-btn filter-btn--danger">None</button>
    <button type="button" onclick="filterInterior('basic', this)" class="filter-btn filter-btn--danger">Basic</button>
    <button type="button" onclick="filterInterior('standard', this)" class="filter-btn filter-btn--danger">Standard</button>
    <button type="button" onclick="filterInterior('deep', this)" class="filter-btn filter-btn--danger">Deep</button>
  </div>
</div>

<div class="filter-section">
  <strong>Size:</strong>
  <div class="filter-group">
    <button type="button" onclick="filterSize('all', this)" class="filter-btn filter-btn--warning is-active" data-filter="all">All</button>
    <button type="button" onclick="filterSize('small', this)" class="filter-btn filter-btn--warning">Small</button>
    <button type="button" onclick="filterSize('medium', this)" class="filter-btn filter-btn--warning">Medium</button>
    <button type="button" onclick="filterSize('large', this)" class="filter-btn filter-btn--warning">Large</button>
    <button type="button" onclick="filterSize('very-large', this)" class="filter-btn filter-btn--warning">Very Large</button>
  </div>
</div>

<div class="filter-section range-slider">
  <strong>Max. Time (hrs):</strong>
  <input type="range" id="timeSlider" min="1" max="8" value="8" step="1"
         oninput="updateTimeFilter(this.value)">
  <span class="range-value" id="timeValue">Up to 8+</span>
</div>

<div class="filter-section range-slider">
  <strong>Max. Price (£):</strong>
  <input type="range" id="priceSlider" min="10" max="200" value="200" step="10"
         oninput="updatePriceFilter(this.value)">
  <span class="range-value" id="priceValue">Up to £200+</span>
</div>

<!-- Service Cards -->
<div id="services-container" style="width:100%;max-width:1000px;margin:0 auto;">
    <div class="service-header">
        <div class="service-col">Service</div>
        <div class="time-col">Time</div>
        <div class="price-col">Price</div>
        <div class="loyalty-col">Loyalty</div>
        <div class="book-col">Book</div>
    </div>

  {% assign rate = site.data.services.hourly_rate %}
  {% assign fixed_charge = site.data.services.fixed_charge | default: 0 %}
  {% assign sizes = site.data.services.sizes %}

  {%- comment -%} -------- Exterior only -------- {%- endcomment -%}
  {% for exterior_level in site.data.services.times.exterior %}
    {% assign ext_key = exterior_level[0] %}
    {% if ext_key != "none" %}
      {% assign int_key = "none" %}
      {% for size in sizes %}
        {% include service_card.html category="exterior" ext_key=ext_key int_key=int_key size=size %}
      {% endfor %}
    {% endif %}
  {% endfor %}

  {%- comment -%} -------- Valets (ext == int) -------- {%- endcomment -%}
  {% for exterior_level in site.data.services.times.exterior %}
    {% assign ext_key = exterior_level[0] %}
    {% if ext_key != "none" and site.data.services.times.interior[ext_key] %}
      {% assign int_key = ext_key %}
      {% for size in sizes %}
        {% include service_card.html category="valet" ext_key=ext_key int_key=int_key size=size %}
      {% endfor %}
    {% endif %}
  {% endfor %}

  {%- comment -%} -------- Mixed (ext != int) -------- {%- endcomment -%}
  {% for exterior_level in site.data.services.times.exterior %}
    {% assign ext_key = exterior_level[0] %}
    {% if ext_key != "none" %}
      {% for interior_level in site.data.services.times.interior %}
        {% assign int_key = interior_level[0] %}
        {% if int_key != "none" and int_key != ext_key %}
          {% for size in sizes %}
            {% include service_card.html category="mixed" ext_key=ext_key int_key=int_key size=size %}
          {% endfor %}
        {% endif %}
      {% endfor %}
    {% endif %}
  {% endfor %}

  {%- comment -%} -------- Interior only -------- {%- endcomment -%}
  {% assign ext_key = "none" %}
  {% for interior_level in site.data.services.times.interior %}
    {% assign int_key = interior_level[0] %}
    {% if int_key != "none" %}
      {% for size in sizes %}
        {% include service_card.html category="interior" ext_key=ext_key int_key=int_key size=size %}
      {% endfor %}
    {% endif %}
  {% endfor %}
</div>

<!-- Filtering Script -->
<script>
let currentCategory = 'all';
let currentExterior = 'all';
let currentInterior = 'all';
let currentSize = 'all';
let currentTime = 8;   // hours
let currentPrice = 200; // £

function filterServices(category, btn) {
  currentCategory = category;
  updateActiveFilter(btn, 'category');
  applyFilters();
}

function filterExterior(depth, btn) {
  currentExterior = depth;
  updateActiveFilter(btn, 'exterior');
  applyFilters();
}

function filterInterior(depth, btn) {
  currentInterior = depth;
  updateActiveFilter(btn, 'interior');
  applyFilters();
}

function filterSize(size, btn) {
  currentSize = size;
  updateActiveFilter(btn, 'size');
  applyFilters();
}

function updateActiveFilter(button, filterType) {
  // Get all buttons in the same filter group (same parent .filter-group)
  const group = button ? button.closest('.filter-group') : null;
  if (group) {
    const buttons = group.querySelectorAll('.filter-btn');
    buttons.forEach(btn => btn.classList.remove('is-active'));
    if (button) button.classList.add('is-active');
  }
}

function updateTimeFilter(val) {
  currentTime = parseInt(val);
  document.getElementById('timeValue').innerText = (val == 8) ? "Up to 8+" : "Up to " + val + " hrs";
  applyFilters();
}

function updatePriceFilter(val) {
  currentPrice = parseInt(val);
  document.getElementById('priceValue').innerText = (val == 200) ? "Up to £200+" : "Up to £" + val;
  applyFilters();
}

function applyFilters() {
  const cards = document.querySelectorAll('.service-card');
  cards.forEach(card => {
    const matchCategory = (currentCategory === 'all' || card.dataset.category === currentCategory);
    const matchExterior = (currentExterior === 'all' || card.dataset.exterior === currentExterior);
    const matchInterior = (currentInterior === 'all' || card.dataset.interior === currentInterior);
    const matchSize = (currentSize === 'all' || card.dataset.size === currentSize);

    const time = parseInt(card.dataset.time);
    const price = parseInt(card.dataset.price);
    const matchTime = (time <= currentTime || currentTime === 8); // 8 means 8+
    const matchPrice = (price <= currentPrice || currentPrice === 200); // 200 means 200+

    card.style.display = (matchCategory && matchExterior && matchInterior && matchSize && matchTime && matchPrice)
      ? 'flex'
      : 'none';
  });
}
</script>


| Extras | Price |
|:---|:---:|
| Panel Polishing (Requires minimum basic exterior additionally, deep exterior highly recommended) | £10 per panel, per stage | 
| Handle polishing (if the parent panel is not polished) | £2.50 per door handle |

Extra Charges:
For every mile more than 10 miles from Base Location (WS11 7YQ): £1 per mile



<script>
function showDescription(text) {
  alert(text);
}
</script>

<script type="text/javascript">
  (function (C, A, L) {
    let p = function (a, ar) { a.q.push(ar); };
    let d = C.document;
    C.Cal = C.Cal || function () {
      let cal = C.Cal; let ar = arguments;
      if (!cal.loaded) {
        cal.ns = {}; cal.q = cal.q || [];
        d.head.appendChild(d.createElement("script")).src = A;
        cal.loaded = true;
      }
      if (ar[0] === L) {
        const api = function () { p(api, arguments); };
        const namespace = ar[1];
        api.q = api.q || [];
        if (typeof namespace === "string") {
          cal.ns[namespace] = cal.ns[namespace] || api;
          p(cal.ns[namespace], ar);
          p(cal, ["initNamespace", namespace]);
        } else p(cal, ar);
        return;
      }
      p(cal, ar);
    };
  })(window, "https://app.cal.com/embed/embed.js", "init");
  Cal("init", { origin: "https://app.cal.com" });
</script>


<div id="serviceModal">
  <div class="modal-box">
    <span class="close-btn" onclick="closeServiceModal()">&times;</span>
    <div id="serviceModalContent" style="white-space:pre-line;"></div>
  </div>
</div>

<script>
function openServiceModal(text) {
  document.getElementById('serviceModalContent').innerText = text;
  document.getElementById('serviceModal').style.display = 'flex';
}
function closeServiceModal() {
  document.getElementById('serviceModal').style.display = 'none';
}
document.getElementById('serviceModal').addEventListener('click', function(e) {
  if (e.target.id === 'serviceModal') closeServiceModal();
});
</script>
