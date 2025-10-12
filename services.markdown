---
layout: page
title: Services and Price List
permalink: /services/
---

## Prices Starting 1st October 2025:

#### Loyalty Discount - Clean again within 3 months to get up to a 15% discount 
 - Interval and discount applies to cars individually

#### Car Categories:
**Small:** Superminis e.g. Ford Fiesta, VW Polo  
**Regular:** Most cars: hatchbacks, SUVs, small estates, saloons, etc.  
**Large:** Any car with a boot over 600 litres and vans smaller than a Ford Transit Custom  
**Very Large:** Cars with three rows of seats and vans a similar size and larger than a Ford Transit Custom  
Note: Only the passenger area in a van is cleaned, not cargo area.  

<h2 style="margin-bottom:1rem;">Car Services</h2>

<!-- Filter Controls -->
<div style="margin-bottom:1rem;">
  <strong>Filter by Category:</strong>
  <button onclick="filterServices('all')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#6c757d;color:#fff;border:none;border-radius:4px;cursor:pointer;">All</button>
  <button onclick="filterServices('exterior')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#28a745;color:#fff;border:none;border-radius:4px;cursor:pointer;">Exterior</button>
  <button onclick="filterServices('valet')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#28a745;color:#fff;border:none;border-radius:4px;cursor:pointer;">Valet</button>
  <button onclick="filterServices('mixed')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#28a745;color:#fff;border:none;border-radius:4px;cursor:pointer;">Mixed</button>
  <button onclick="filterServices('interior')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#28a745;color:#fff;border:none;border-radius:4px;cursor:pointer;">Interior</button>
</div>

<div style="margin-bottom:1rem;">
  <strong>Filter by Exterior:</strong>
  <button onclick="filterExterior('all')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#6c757d;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    All
  </button>
  <button onclick="filterExterior('none')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#2196f3;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    None
  </button>
  <button onclick="filterExterior('basic')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#2196f3;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    Basic
  </button>
  <button onclick="filterExterior('standard')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#2196f3;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    Standard
  </button>
  <button onclick="filterExterior('deep')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#2196f3;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    Deep
  </button>
</div>

<div style="margin-bottom:1rem;">
  <strong>Filter by Interior:</strong>
  <button onclick="filterInterior('all')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#6c757d;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    All
  </button>
  <button onclick="filterInterior('none')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#B22222;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    None
  </button>
  <button onclick="filterInterior('basic')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#B22222;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    Basic
  </button>
  <button onclick="filterInterior('standard')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#B22222;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    Standard
  </button>
  <button onclick="filterInterior('deep')"
          style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
                 background:#B22222;color:#fff;border:none;border-radius:4px;cursor:pointer;">
    Deep
  </button>
</div>

<div style="margin-bottom:1rem;">
  <strong>Filter by Size:</strong>
  <button onclick="filterSize('all')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#6c757d;color:#fff;border:none;border-radius:4px;cursor:pointer;">All</button>
  <button onclick="filterSize('small')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#9c27b0;color:#fff;border:none;border-radius:4px;cursor:pointer;">Small</button>
  <button onclick="filterSize('medium')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#9c27b0;color:#fff;border:none;border-radius:4px;cursor:pointer;">Medium</button>
  <button onclick="filterSize('large')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#9c27b0;color:#fff;border:none;border-radius:4px;cursor:pointer;">Large</button>
  <button onclick="filterSize('very-large')" style="display:inline-block;padding:0.4rem 0.8rem;margin:0.2rem;
               background:#9c27b0;color:#fff;border:none;border-radius:4px;cursor:pointer;">Very Large</button>
</div>

<div style="margin-bottom:1rem;">
  <strong>Filter by Time (hrs):</strong>
  <input type="range" id="timeSlider" min="1" max="8" value="8" step="1"
         oninput="updateTimeFilter(this.value)"
         style="width:200px;">
  <span id="timeValue">Up to 8+</span>
</div>

<div style="margin-bottom:1rem;">
  <strong>Filter by Price (£):</strong>
  <input type="range" id="priceSlider" min="10" max="200" value="200" step="10"
         oninput="updatePriceFilter(this.value)"
         style="width:200px;">
  <span id="priceValue">Up to £200+</span>
</div>

<!-- Service Cards -->
<div id="services-container" style="width:100%;max-width:1000px;margin:0 auto;">
    <div style="display:flex;flex-wrap:wrap;align-items:center;gap:8px;font-weight:bold;border-bottom:2px solid #ccc;padding:0.5rem 0;">
    <div style="flex:1;min-width:200px;white-space:nowrap;">Service</div>
    <div style="flex:0 0 80px;text-align:center;white-space:nowrap;">Time</div>
    <div style="flex:0 0 80px;text-align:center;white-space:nowrap;">Price</div>
    <div style="flex:0 0 100px;text-align:center;white-space:nowrap;">Loyalty</div>
    <div style="flex:0 0 100px;text-align:center;white-space:nowrap;">Book</div>
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

function filterServices(category) { currentCategory = category; applyFilters(); }
function filterExterior(depth) { currentExterior = depth; applyFilters(); }
function filterInterior(depth) { currentInterior = depth; applyFilters(); }
function filterSize(size) { currentSize = size; applyFilters(); }

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


<!-- Service Description Modal -->
<div id="serviceModal" style="display:none;position:fixed;top:0;left:0;width:100%;height:100%;
     background:rgba(0,0,0,0.6);z-index:9999;align-items:center;justify-content:center;">
  <div style="background:#fff;padding:1.5rem;border-radius:8px;max-width:500px;width:90%;position:relative;">
    <span onclick="closeServiceModal()" 
          style="position:absolute;top:0.5rem;right:0.75rem;cursor:pointer;font-size:1.2rem;font-weight:bold;">&times;</span>
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
// Optional: close when clicking outside the box
document.getElementById('serviceModal').addEventListener('click', function(e) {
  if (e.target.id === 'serviceModal') closeServiceModal();
});
</script>