{% if site.elsewhere_email | size %}
<li class="email wide">{{ site.elsewhere_email }}</li>
{% endif %}
{% if site.elsewhere_dribbble | size %}
<li class="dribbble"><a href="{{ site.elsewhere_dribbble }}" title="A taste of things to come">Dribbble</a></li>
{% endif %}   
{% if site.elsewhere_github | size %}
<li class="github"><a href="{{ site.elsewhere_github }}" title="Snoop around my code">GitHub</a></li>
{% endif %}
{% if site.elsewhere_linkedin | size %}
<li class="linkedin"><a href="{{ site.elsewhere_linkedin }}" title="See what I've done professionally">LinkedIn</a></li>
{% endif %}
{% if site.elsewhere_meetup | size %}
<li class="meetup"><a href="{{ site.elsewhere_meetup }}" title="Find me out and about">Meetup</a></li>
{% endif %}
{% if site.elsewhere_spotify | size %}
<li class="spotify"><a href="{{ site.elsewhere_spotify }}" title="Listen to my selected sounds">Spotify</a></li>
{% endif %}
{% if site.elsewhere_twitter | size %}
<li class="twitter"><a href="{{ site.elsewhere_twitter }}" title="Follow my shortened ramblings">Twitter</a></li>
{% endif %}
{% if site.elsewhere_rss | size %}
<li class="rss"><a href="{{ site.elsewhere_rss }}" title="Hot off the press RSS">RSS</a></li>
{% endif %}
