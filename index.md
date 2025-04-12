---
title: an umbreon on the FUCKING internet
content-updated: 2024-11-07
style: |
    .buttons {
        display: flex;
        flex-wrap: wrap;
        gap: 0.5em;
    }
---
# Hey Erin What The Fuck Is This

yeah this is just a silly little website for hosting silly things that come out of my extremely silly brain. i probably wont ever make this homepage any better than it is right now because im a lazy fuck but maybe if i ever do anything neat ill host it here and then you can read it

## Some Bullshit You Can Find Here

<ul>
{%- assign sorted_posts = site.posts | sort: "date" -%}
{%- for p in sorted_posts %}
	{% assign title = p.title -%}
	{%- if p.title_md %}{% assign title = p.title_md | markdownify | remove: "<p>" | remove: "</p>" | strip %}{% endif -%}
	<li><a href="{{p.permalink | default: p.url}}">{{title}}</a></li>
{% endfor -%}
</ul>

## by the way who the fuck are you
my name is erin and i am <a rel="me" href="https://tired.umbreon.online/@erin">@erin@tired.umbreon.online</a> on the fediverse and i dont exist anywhere else (this is sarcasm i do have other accounts but i try to avoid linking to all my online presences from each other. if you know me from somewhere else no u dont)

i use it/its pronouns. if you know me from somewhere else where i list she/her pronouns i also use those but i dont like them very much and nowadays i mostly just use them with ppl who arent sufficiently Gender

im a web developer type person except for that last part. i mostly know too much css and am on a mission to be bad at every frontend framework. i also work on browser extensions which means i have an above-average amount of hatred in my heart for google chrome

i also run [webring.umbreon.online](https://webring.umbreon.online) and have some of my code stuff on my [personal git server](https://git.ewin.moe/erin) (or [my personal github account](https://github.com/ewwwin) which pretty much only has github pages sites like this one in it)

other than that im kind of boring. local chronically sleepy transfem doesnt have interesting content for website homepage, more at 11. check out the webring for more sites run by cool folks

## it is the current year and this is a queer personal website, where the heck are the 88x31s

<div class="buttons">
    <picture onclick="alert('hehe that tickles')">
        <source
            media="(prefers-reduced-motion)"
            srcset="/assets/88x31/umbreon_dot_online_static.gif"
        >
        <img
            alt="umbreon.online"
            title="umbreon.online"
            src="/assets/88x31/umbreon_dot_online.gif"
        >
    </picture>
    <a href="https://tempest.dev">
        <img
            alt="tempest.dev"
            title="tempest.dev"
            src="/assets/88x31/tempest.dev.png"
        >
    </a>
    <a href="https://elke.cafe">
        <img
            alt="elke.cafe"
            title="elke.cafe"
            src="/assets/88x31/elke.cafe.gif"
        >
    </a>
    <a href="https://astrid.tech">
        <img
            alt="astrid.tech"
            title="astrid.tech"
            src="/assets/88x31/astriddottech.png"
        >
    </a>
    <a href="https://0x0079.codeberg.page">
        <img
            alt="40796c19"
            title="40796c19"
            src="/img/88x31/40796c19.png"
        >
    </a>
    <a href="https://stella.lifeless.space">
        <img
            alt="void priestess stella"
            title="void priestess stella"
            src="/img/88x31/0x57e11a.png"
        >
    </a>
</div>

if you are a friend and you want to exchange buttons poke me on fedi or something. i like buttons
