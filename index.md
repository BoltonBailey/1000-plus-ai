---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: plain
---

# 1000+ formalizations

{% assign sorted = site.thm | sort: "wikidata" %}
{% assign stated_count = 0 %}
{% assign proved_count = 0 %}
{% for t in sorted %}
            {% assign forms = "" | split: "" %}
            {% if t.isabelle %}{% assign forms = forms | concat: t.isabelle %}{% endif %}
            {% if t.hol_light %}{% assign forms = forms | concat: t.hol_light %}{% endif %}
            {% if t.rocq %}{% assign forms = forms | concat: t.rocq %}{% endif %}
            {% if t.lean %}{% assign forms = forms | concat: t.lean %}{% endif %}
            {% if t.metamath %}{% assign forms = forms | concat: t.metamath %}{% endif %}
            {% if t.mizar %}{% assign forms = forms | concat: t.mizar %}{% endif %}
            {% assign stated = false %}
            {% assign proved = false %}
            {% for f in forms %}
              {% if f.status == "formalized" %}{% assign proved = true %}{% assign stated = true %}{% endif %}
              {% if f.status == "statement" %}{% assign stated = true %}{% endif %}
            {% endfor %}
    {% if stated %}{% assign stated_count = stated_count | plus: 1 %}{% endif %}
    {% if proved %}{% assign proved_count = proved_count | plus: 1 %}{% endif %}
{% endfor %}

<p class="view-tabs">
  <button type="button" class="view-tab active" data-view="all">All ({{ sorted.size }})</button>
  <button type="button" class="view-tab" data-view="stated">Formally stated ({{ stated_count }})</button>
  <button type="button" class="view-tab" data-view="proved">Formally proved ({{ proved_count }})</button>
</p>


<table class="display datatable" data-order-columns="[1]">
    <thead>
        <tr>
            <th class="dt-head-center">MSC</th>
            <th>Name</th>
            <th class="dt-head-center">Isabelle</th>
            <th class="dt-head-center">HOL Light</th>
            <th class="dt-head-center">Rocq</th>
            <th class="dt-head-center">Lean</th>
            <th class="dt-head-center">Metamath</th>
            <th class="dt-head-center">Mizar</th>
        </tr>
    </thead>
    <tbody>
        {% for t in sorted %}
            {% assign forms = "" | split: "" %}
            {% if t.isabelle %}{% assign forms = forms | concat: t.isabelle %}{% endif %}
            {% if t.hol_light %}{% assign forms = forms | concat: t.hol_light %}{% endif %}
            {% if t.rocq %}{% assign forms = forms | concat: t.rocq %}{% endif %}
            {% if t.lean %}{% assign forms = forms | concat: t.lean %}{% endif %}
            {% if t.metamath %}{% assign forms = forms | concat: t.metamath %}{% endif %}
            {% if t.mizar %}{% assign forms = forms | concat: t.mizar %}{% endif %}
            {% assign stated = false %}
            {% assign proved = false %}
            {% for f in forms %}
              {% if f.status == "formalized" %}{% assign proved = true %}{% assign stated = true %}{% endif %}
              {% if f.status == "statement" %}{% assign stated = true %}{% endif %}
            {% endfor %}
            <tr id="{{ t.wikidata }}" data-stated="{{ stated }}" data-proved="{{ proved }}">
                <td class="dt-body-center"><span title="{{ site.data.msc[t.msc_classification] }}">{{ t.msc_classification }}</span></td>
                <td>
                    {% assign wl = t.wikipedia_links.first %}
                    {% if wl contains "|" %}
                        {% assign wl_parts = wl | split: '|' %}
                        {% assign wlabel = wl_parts[1] | remove: ']]' %}
                        {% assign wurl = wl_parts[0] | remove: '[[' %}
                    {% else %}
                        {% assign wlabel = wl | remove: '[[' | remove: ']]' %}
                        {% assign wurl = wlabel %}
                    {% endif %}
                    <a href="https://en.wikipedia.org/wiki/{{ wurl }}" title="Wikidata ID {{ t.wikidata }}">{{ wlabel }}</a>
                </td>
                <td class="dt-body-center">
                    {% if t.isabelle %}
                        {% for f in t.isabelle %}
                            {% unless forloop.first %}<br>{% endunless %}
                            {% if f.status == "not_found" %}
                            <span class="notfound" title="searched, not found">&mdash;</span>
                            {% elsif f.status == "statement" %}
                            <a class="stmt" href="{{ f.url }}" title="statement only{% if f.authors and f.authors != empty %} — {{ f.authors | join: ', ' }}{% endif %}">({% include lib_name.html f=f %})</a>
                            {% else %}
                            <a href="{{ f.url }}" title="{{ f.authors | join: ', ' }}">{% include lib_name.html f=f %}</a>
                            {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                        {% endfor %}
                    {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                </td>
                <td class="dt-body-center">
                    {% if t.hol_light %}
                        {% for f in t.hol_light %}
                            {% unless forloop.first %}<br>{% endunless %}
                            {% if f.status == "not_found" %}
                            <span class="notfound" title="searched, not found">&mdash;</span>
                            {% elsif f.status == "statement" %}
                            <a class="stmt" href="{{ f.url }}" title="statement only{% if f.authors and f.authors != empty %} — {{ f.authors | join: ', ' }}{% endif %}">({% include lib_name.html f=f %})</a>
                            {% else %}
                            <a href="{{ f.url }}" title="{{ f.authors | join: ', ' }}">{% include lib_name.html f=f %}</a>
                            {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                        {% endfor %}
                    {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                </td>
                <td class="dt-body-center">
                    {% if t.rocq %}
                        {% for f in t.rocq %}
                            {% unless forloop.first %}<br>{% endunless %}
                            {% if f.status == "not_found" %}
                            <span class="notfound" title="searched, not found">&mdash;</span>
                            {% elsif f.status == "statement" %}
                            <a class="stmt" href="{{ f.url }}" title="statement only{% if f.authors and f.authors != empty %} — {{ f.authors | join: ', ' }}{% endif %}">({% include lib_name.html f=f %})</a>
                            {% else %}
                            <a href="{{ f.url }}" title="{{ f.authors | join: ', ' }}">{% include lib_name.html f=f %}</a>
                            {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                        {% endfor %}
                    {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                </td>
                <td class="dt-body-center">
                    {% if t.lean %}
                        {% for f in t.lean %}
                            {% unless forloop.first %}<br>{% endunless %}
                            {% if f.status == "not_found" %}
                            <span class="notfound" title="searched, not found">&mdash;</span>
                            {% elsif f.status == "statement" %}
                            <a class="stmt" href="{{ f.url }}" title="statement only{% if f.authors and f.authors != empty %} — {{ f.authors | join: ', ' }}{% endif %}">({% include lib_name.html f=f %})</a>
                            {% else %}
                            <a href="{{ f.url }}" title="{{ f.authors | join: ', ' }}">{% include lib_name.html f=f %}</a>
                            {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                        {% endfor %}
                    {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                </td>
                <td class="dt-body-center">
                    {% if t.metamath %}
                        {% for f in t.metamath %}
                            {% unless forloop.first %}<br>{% endunless %}
                            {% if f.status == "not_found" %}
                            <span class="notfound" title="searched, not found">&mdash;</span>
                            {% elsif f.status == "statement" %}
                            <a class="stmt" href="{{ f.url }}" title="statement only{% if f.authors and f.authors != empty %} — {{ f.authors | join: ', ' }}{% endif %}">({% include lib_name.html f=f %})</a>
                            {% else %}
                            <a href="{{ f.url }}" title="{{ f.authors | join: ', ' }}">{% include lib_name.html f=f %}</a>
                            {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                        {% endfor %}
                    {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                </td>
                <td class="dt-body-center">
                    {% if t.mizar %}
                        {% for f in t.mizar %}
                            {% unless forloop.first %}<br>{% endunless %}
                            {% if f.status == "not_found" %}
                            <span class="notfound" title="searched, not found">&mdash;</span>
                            {% elsif f.status == "statement" %}
                            <a class="stmt" href="{{ f.url }}" title="statement only{% if f.authors and f.authors != empty %} — {{ f.authors | join: ', ' }}{% endif %}">({% include lib_name.html f=f %})</a>
                            {% else %}
                            <a href="{{ f.url }}" title="{{ f.authors | join: ', ' }}">{% include lib_name.html f=f %}</a>
                            {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                        {% endfor %}
                    {% else %}
                        <span class="unknown" title="not checked yet">?</span>
                    {% endif %}
                </td>
            </tr>
        {% endfor %}
    </tbody>
</table>

## Guide

<ul class="table-legend">
  <li>Each cell names the library or repository containing the formalization, and links to it.</li>
  <li>A name in parentheses, e.g. <a class="stmt" href="#">(lean-eval)</a>, means only the <em>statement</em> has been formalized, not the proof.</li>
  <li><span class="unknown">?</span> — no check or search has been run for a formalization yet.</li>
  <li><span class="notfound">&mdash;</span> — a formalization was searched for but not found.</li>
</ul>
