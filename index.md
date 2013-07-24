---
layout: page
---
<div class="hfeed">
{% for post in paginator.posts %}
    <div class="hentry">
        <h2 class="entry-title"><a href="{{ site.production_url }}{{ post.url }}" rel="bookmark">{{ post.title }}</a></h2>
        <ul class="inline">
            {% if post.author %}<li><span class="vcard"><i class="icon-user"></i> <span class="fn">{{ post.author }}</span></span></li>{% endif %}
            {% if post.date %}<li><abbr class="published" title="{{ post.date | date: "%a, %d %b %Y %H:%M:%S %z" }}"><i class="icon-calendar"></i> {{ post.date | date: "%b %d, %Y" }}</abbr></li>{% endif %}
            {% if site.comments.provider %}<li><i class="icon-comment"></i> <a href="{{ site.production_url }}{{ post.url }}#disqus_thread">Comment</a></li>{% endif %}
        </ul>
        <p class="entry-summary">{{ post.content | strip_html | truncatewords: 50 }}</p>
        <p><a href="{{ site.production_url }}{{ post.url }}" rel="nofollow">Read more</a></p>
    </div>
{% endfor %}
</div>

<div class="pagination">
<ul>
    {% if paginator.previous_page %}
    {% if paginator.previous_page == 1 %}
        <li><a href="{{ site.production_url }}/">Prev</a></li>
    {% else %}
        <li><a href="{{ site.prudoction_url }}/page{{ paginator.previous_page }}">Prev</a></li>
    {% endif %}
    {% else %}
        <li><span class="disabled">Prev</span></li>
    {% endif %}

    
    {% if paginator.next_page %}
        <li><a href="{{ site.production_url }}/page{{ paginator.next_page }}">Next</a></li>
    {% else %}
        <li><span class="disabled">Next</span></li>
    {% endif %}
</ul>
</div>
