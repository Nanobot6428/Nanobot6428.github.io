<h3>Car Services</h3>
<table class="service-table">
  <thead>
    <tr>
      <th>Service</th>
      <th>Size</th>
      <th>Time (hrs)</th>
      <th>Full Price (£)</th>
      <th>Loyalty Price (£)</th>
      <th>Book</th>
    </tr>
  </thead>
  <tbody>
    {% assign rate = site.data.services.hourly_rate %}
    {% assign fixed_charge = site.data.services.fixed_charge | default: 0 %}
    {% assign sizes = site.data.services.sizes %}

    {%- comment -%} ---------- EXTERIOR ONLY ---------- {%- endcomment -%}
    <tr class="group-header">
      <td colspan="6"><strong>Exterior Only</strong></td>
    </tr>
    {% for exterior_level in site.data.services.times.exterior %}
      {% assign ext_key = exterior_level[0] %}
      {% if ext_key != "none" %}
        {% assign int_key = "none" %}
        {% for size in sizes %}
          {% assign ext_size_ratio = site.data.services.ratios.exterior[size.key] %}
          {% assign int_size_ratio = site.data.services.ratios.interior[size.key] %}

          {% assign ext_time_base = site.data.services.times.exterior[ext_key] %}
          {% assign int_time_base = site.data.services.times.interior[int_key] %}
          {% assign ext_cost_base = site.data.services.costs.exterior[ext_key] %}
          {% assign int_cost_base = site.data.services.costs.interior[int_key] %}

          {% assign ext_time_scaled = ext_time_base | times: ext_size_ratio %}
          {% assign int_time_scaled = int_time_base | times: int_size_ratio %}
          {% assign total_time = ext_time_scaled | plus: int_time_scaled %}

          {% assign ext_labour = ext_time_base | times: rate | times: ext_size_ratio %}
          {% assign ext_chems  = ext_cost_base | times: ext_size_ratio %}
          {% assign ext_total  = ext_labour | plus: ext_chems %}

          {% assign int_labour = int_time_base | times: rate | times: int_size_ratio %}
          {% assign int_chems  = int_cost_base | times: int_size_ratio %}
          {% assign int_total  = int_labour | plus: int_chems %}

          {% assign full_price = ext_total | plus: int_total | plus: fixed_charge %}
          {% assign discounted = full_price | times: 0.85 %}

          {% assign pretty_service = ext_key | capitalize | append: " Exterior" %}
          {% assign pretty_name = size.name | append: " " | append: pretty_service %}

          <tr>
            {% if forloop.first %}
              <td rowspan="{{ sizes | size }}">
                <strong>{{ pretty_service }}</strong><br>
                {% if site.data.services.descriptions.exterior[ext_key] %}
                  <em>{{ site.data.services.descriptions.exterior[ext_key] }}</em>
                {% endif %}
              </td>
            {% endif %}
            <td>{{ size.name }}</td>
            <td>{{ total_time | round: 1 }}</td>
            <td>£{{ full_price | round }}</td>
            <td>£{{ discounted | round }}</td>
            <td>
              <a href="https://cal.com/rwmvaleting/{{ size.key }}-{{ ext_key }}-none">
                Book {{ size.name }}
              </a>
            </td>
          </tr>
        {% endfor %}
      {% endif %}
    {% endfor %}

    {%- comment -%} ---------- VALETS (ext_key == int_key, not none) ---------- {%- endcomment -%}
    <tr class="group-header">
      <td colspan="6"><strong>Valets</strong></td>
    </tr>
    {% for exterior_level in site.data.services.times.exterior %}
      {% assign ext_key = exterior_level[0] %}
      {% if ext_key != "none" %}
        {% for interior_level in site.data.services.times.interior %}
          {% assign int_key = interior_level[0] %}
          {% if int_key == ext_key and int_key != "none" %}
            {% for size in sizes %}
              {% assign ext_size_ratio = site.data.services.ratios.exterior[size.key] %}
              {% assign int_size_ratio = site.data.services.ratios.interior[size.key] %}

              {% assign ext_time_base = site.data.services.times.exterior[ext_key] %}
              {% assign int_time_base = site.data.services.times.interior[int_key] %}
              {% assign ext_cost_base = site.data.services.costs.exterior[ext_key] %}
              {% assign int_cost_base = site.data.services.costs.interior[int_key] %}

              {% assign ext_time_scaled = ext_time_base | times: ext_size_ratio %}
              {% assign int_time_scaled = int_time_base | times: int_size_ratio %}
              {% assign total_time = ext_time_scaled | plus: int_time_scaled %}

              {% assign ext_labour = ext_time_base | times: rate | times: ext_size_ratio %}
              {% assign ext_chems  = ext_cost_base | times: ext_size_ratio %}
              {% assign ext_total  = ext_labour | plus: ext_chems %}

              {% assign int_labour = int_time_base | times: rate | times: int_size_ratio %}
              {% assign int_chems  = int_cost_base | times: int_size_ratio %}
              {% assign int_total  = int_labour | plus: int_chems %}

              {% assign full_price = ext_total | plus: int_total | plus: fixed_charge %}
              {% assign discounted = full_price | times: 0.85 %}

              {% assign pretty_service = size.name | append: " " | append: ext_key | capitalize | append: " Valet" %}

              <tr>
                {% if forloop.first %}
                  <td rowspan="{{ sizes | size }}">
                    <strong>{{ ext_key | capitalize }} Valet</strong><br>
                    {% if site.data.services.descriptions.valet and site.data.services.descriptions.valet[ext_key] %}
                      <em>{{ site.data.services.descriptions.valet[ext_key] }}</em>
                    {% else %}
                      {% if site.data.services.descriptions.exterior[ext_key] %}
                        <em>{{ site.data.services.descriptions.exterior[ext_key] }}</em><br>
                      {% endif %}
                      {% if site.data.services.descriptions.interior[int_key] %}
                        <em>{{ site.data.services.descriptions.interior[int_key] }}</em>
                      {% endif %}
                    {% endif %}
                  </td>
                {% endif %}
                <td>{{ size.name }}</td>
                <td>{{ total_time | round: 1 }}</td>
                <td>£{{ full_price | round }}</td>
                <td>£{{ discounted | round }}</td>
                <td>
                  <a href="https://cal.com/rwmvaleting/{{ size.key }}-{{ ext_key }}-{{ int_key }}">
                    Book {{ size.name }}
                  </a>
                </td>
              </tr>
            {% endfor %}
          {% endif %}
        {% endfor %}
      {% endif %}
    {% endfor %}

    {%- comment -%} ---------- MIXED EXTERIOR + INTERIOR (different depths) ---------- {%- endcomment -%}
    <tr class="group-header">
      <td colspan="6"><strong>Exterior + Interior (Mixed)</strong></td>
    </tr>
    {% for exterior_level in site.data.services.times.exterior %}
      {% assign ext_key = exterior_level[0] %}
      {% if ext_key != "none" %}
        {% for interior_level in site.data.services.times.interior %}
          {% assign int_key = interior_level[0] %}
          {% if int_key != "none" and int_key != ext_key %}
            {% for size in sizes %}
              {% assign ext_size_ratio = site.data.services.ratios.exterior[size.key] %}
              {% assign int_size_ratio = site.data.services.ratios.interior[size.key] %}

              {% assign ext_time_base = site.data.services.times.exterior[ext_key] %}
              {% assign int_time_base = site.data.services.times.interior[int_key] %}
              {% assign ext_cost_base = site.data.services.costs.exterior[ext_key] %}
              {% assign int_cost_base = site.data.services.costs.interior[int_key] %}

              {% assign ext_time_scaled = ext_time_base | times: ext_size_ratio %}
              {% assign int_time_scaled = int_time_base | times: int_size_ratio %}
              {% assign total_time = ext_time_scaled | plus: int_time_scaled %}

              {% assign ext_labour = ext_time_base | times: rate | times: ext_size_ratio %}
              {% assign ext_chems  = ext_cost_base | times: ext_size_ratio %}
              {% assign ext_total  = ext_labour | plus: ext_chems %}

              {% assign int_labour = int_time_base | times: rate | times: int_size_ratio %}
              {% assign int_chems  = int_cost_base | times: int_size_ratio %}
              {% assign int_total  = int_labour | plus: int_chems %}

              {% assign full_price = ext_total | plus: int_total | plus: fixed_charge %}
              {% assign discounted = full_price | times: 0.85 %}

              {% assign pretty_service_human = ext_key | capitalize | append: " Exterior + " | append: int_key | capitalize | append: " Interior" %}
              {% assign pretty_service = size.name | append: " " | append: pretty_service_human %}

              <tr>
                {% if forloop.first %}
                  <td rowspan="{{ sizes | size }}">
                    <strong>{{ pretty_service_human }}</strong><br>
                    {% if site.data.services.descriptions.exterior[ext_key] %}
                      <em>{{ site.data.services.descriptions.exterior[ext_key] }}</em><br>
                    {% endif %}
                    {% if site.data.services.descriptions.interior[int_key] %}
                      <em>{{ site.data.services.descriptions.interior[int_key] }}</em>
                    {% endif %}
                  </td>
                {% endif %}
                <td>{{ size.name }}</td>
                <td>{{ total_time | round: 1 }}</td>
                <td>£{{ full_price | round }}</td>
                <td>£{{ discounted | round }}</td>
                <td>
                  <a href="https://cal.com/rwmvaleting/{{ size.key }}-{{ ext_key }}-{{ int_key }}">
                    Book {{ size.name }}
                  </a>
                </td>
              </tr>
            {% endfor %}
          {% endif %}
        {% endfor %}
      {% endif %}
    {% endfor %}

    {%- comment -%} ---------- INTERIOR ONLY (always last) ---------- {%- endcomment -%}
    <tr class="group-header">
      <td colspan="6"><strong>Interior Only</strong></td>
    </tr>
    {% assign ext_key = "none" %}
    {% for interior_level in site.data.services.times.interior %}
      {% assign int_key = interior_level[0] %}
      {% if int_key != "none" %}
        {% for size in sizes %}
          {% assign ext_size_ratio = site.data.services.ratios.exterior[size.key] %}
          {% assign int_size_ratio = site.data.services.ratios.interior[size.key] %}

          {% assign ext_time_base = site.data.services.times.exterior[ext_key] %}
          {% assign int_time_base = site.data.services.times.interior[int_key] %}
          {% assign ext_cost_base = site.data.services.costs.exterior[ext_key] %}
          {% assign int_cost_base = site.data.services.costs.interior[int_key] %}

          {% assign ext_time_scaled = ext_time_base | times: ext_size_ratio %}
          {% assign int_time_scaled = int_time_base | times: int_size_ratio %}
          {% assign total_time = ext_time_scaled | plus: int_time_scaled %}

          {% assign ext_labour = ext_time_base | times: rate | times: ext_size_ratio %}
          {% assign ext_chems  = ext_cost_base | times: ext_size_ratio %}
          {% assign ext_total  = ext_labour | plus: ext_chems %}

          {% assign int_labour = int_time_base | times: rate | times: int_size_ratio %}
          {% assign int_chems  = int_cost_base | times: int_size_ratio %}
          {% assign int_total  = int_labour | plus: int_chems %}

          {% assign full_price = ext_total | plus: int_total | plus: fixed_charge %}
          {% assign discounted = full_price | times: 0.85 %}

          {% assign pretty_service_human = int_key | capitalize | append: " Interior" %}
          {% assign pretty_service = size.name | append: " " | append: pretty_service_human %}

          <tr>
            {% if forloop.first %}
              <td rowspan="{{ sizes | size }}">
                <strong>{{ pretty_service_human }}</strong><br>
                {% if site.data.services.descriptions.interior[int_key] %}
                  <em>{{ site.data.services.descriptions.interior[int_key] }}</em>
                {% endif %}
              </td>
            {% endif %}
            <td>{{ size.name }}</td>
            <td>{{ total_time | round: 1 }}</td>
            <td>£{{ full_price | round }}</td>
            <td>£{{ discounted | round }}</td>
            <td>
              <a href="https://cal.com/rwmvaleting/{{ size.key }}-none-{{ int_key }}">
                Book {{ size.name }}
              </a>
            </td>
          </tr>
        {% endfor %}
      {% endif %}
    {% endfor %}
  </tbody>
</table>