---
layout: default
title: Blog Archive
permalink: /archive/
---

<main class="content fade-in-down delay-0_75s">
    <div class="inner">
        <header class="page-header">
            <h1 class="page-title">Blog Archive</h1>
            <p class="page-description">A collection of my thoughts and experiences over the years.</p>
        </header>

        <div class="posts-list">
            {% for post in site.posts %}
            <article class="post-summary" style="border-bottom: 1px solid #eee; padding: 2rem 0; margin-bottom: 2rem;">
                <header class="post-header">
                    <h2 class="post-title" style="margin-bottom: 0.5rem;">
                        <a href="{{ post.url | prepend: site.baseurl }}" rel="bookmark" style="color: #333; text-decoration: none;">{{ post.title }}</a>
                    </h2>
                    <div class="post-meta" style="color: #666; font-size: 0.9rem; margin-bottom: 1rem;">
                        <time class="post-date" datetime="{{ post.date | date: "%Y-%m-%d" }}">
                            {{ post.date | date: "%B %d, %Y" }}
                        </time>
                        {% if post.tags.size > 0 %}
                        <span class="post-tags" style="margin-left: 1rem;">
                            {% for tag in post.tags %}
                            <span class="tag" style="background: #f0f0f0; padding: 0.2rem 0.5rem; margin-right: 0.5rem; border-radius: 3px; font-size: 0.8rem;">{{ tag }}</span>
                            {% endfor %}
                        </span>
                        {% endif %}
                    </div>
                </header>
                {% if post.excerpt %}
                <div class="post-excerpt" style="color: #555; line-height: 1.6;">
                    {{ post.excerpt | strip_html | truncatewords: 30 }}
                    <a href="{{ post.url | prepend: site.baseurl }}" style="color: #007acc; text-decoration: none;">Read more →</a>
                </div>
                {% endif %}
            </article>
            {% endfor %}
        </div>
        
        <div style="text-align: center; padding: 2rem 0; color: #666;">
            <p>{{ site.posts.size }} posts total</p>
        </div>
    </div><!-- .inner -->
</main><!-- .content -->