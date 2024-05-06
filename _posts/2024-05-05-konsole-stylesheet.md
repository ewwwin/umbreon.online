---
permalink: /konsole-css
title: A Minimal Konsole Tab Bar Stylesheet
style: |
    :root {
        --theme-light-text-color: hsla(103, 100%, 4%, 0.9);
        --theme-light-body-background:
            linear-gradient(50deg,  hsla(245,60%,87.3%,0.9), transparent 50%),
            linear-gradient(180deg, hsla(257,60%,87.3%,0.9), transparent 66%),
            linear-gradient(290deg, hsla(180,60%,87.3%,0.9), transparent 66%),
            white;
        --theme-dark-text-color: hsla(103, 100%, 97%, 0.9);
        --theme-dark-body-background:
            linear-gradient(50deg,  hsla(245,60%,13.7%,0.9), transparent 75%),
            linear-gradient(180deg, hsla(257,60%,13.7%,0.9), transparent 66%),
            linear-gradient(290deg, hsla(180,60%,8.7%,0.9), transparent 78%),
            black;
    }
---

# Hey Did You Know Konsole Supports Custom Stylesheets

well, it kind of does, anyway! it supports [Qt Stylesheets](https://doc.qt.io/qt-5/stylesheet.html) which are kind of a cursed abomination on top of CSS but it's fine. it's good enough to let me make my tabs look like this:

{% include image.html
	src="/assets/konsolething.png"
	alt="screenshot of my konsole setup. there are three tabs along the bottom edge of the window, with background, font, and color matching the rest of the terminal. the selected tab's text is bold and purple, with a matching purple border on top to distinguish it"
%}

without further ado, here is the CSS. save it in a `.css` file and set it in Konsole settings > Tab Bar / Splitters > Miscellaneous: Use user-defined stylesheet.

```css
/* tabs.css */

QTabWidget::pane {
	border: 0;
}
QTabWidget::tab-bar {
	left: 0;
	right: 0;
}

QTabBar {
	/* adjust to match your terminal font settings */
	font-family: "Comic Code Ligatures";
	font-size: 10pt;
	/* adjust to match your terminal background color */
	/* as far as i'm aware it's not possible to just set this to transparent */
	background: #2C2C2C;
	/* this gets rid of a weird mysterious border that shows up otherwise */
	/* tbh it looks kinda nice but it's not what i'm going for. mess around */
	color: transparent;
}
QTabBar::tab {
	/* 10px is my profile's margin. 13px is that plus some alignment fudge */
	padding: 10px 13px;
	/* change this to border-bottom if you keep tabs on the top */
	border-top: 1px solid transparent;
	background: transparent;
	/* adjust to match your terminal foreground color */
	color: #DCDCCC;
}

/* palette(highlight) tells QT to use the system accent color */
QTabBar::tab:selected {
	font-weight: bold;
	color: palette(highlight);
}
QTabWidget QTabBar::tab:selected {
	border-color: palette(highlight);
}
```

those don't look like normal css selectors, do they! i don't like this tool

konsole doesn't really have any documentation about what the control structure of its UI is so you sort of have to figure it out yourself by reading the source code. which sucks for me because i haven't written or looked at C++ since i finished my CS courses in uni. i wanted to try using a qt inspector tool like [GammaRay](https://github.com/KDAB/GammaRay/releases) but because of packaging shenanigans i couldn't get it working with a simple `dnf install` and was too lazy to put more effort into it

eventually i may put more work into looking at what the tree is like because that would also let me style things like the split-view tab headers. thats like the one big thing left that this theme doesnt really cover; but i dont really use that stuff so for now i just kinda dont care about it

in case you want to mess with something like this yourself, [this is probably the most useful reference page that exists for styling Qt controls](https://doc.qt.io/qt-5/stylesheet-reference.html#tab-sub) - it lists all the widgets and what states/sub-widgets they have, as well as which rules are valid for which widgets and stuff like that. it also links to some examples. basically all the rest of the documentation around this is Not Good and this is the only thing I really looked at while i was working on this (that plus, again, the [konsole source code](https://github.com/KDE/konsole/tree/6c882453da71f7907b3cf345a1af0cd74bd71e26/src) - most of the stuff you'll care about is in `src/widgets`, i also poked at `src/terminalDisplay` a bit but didn't end up doing much with that)

if you know anything else about using Qt stylesheets with Konsole please let me know! i would like to be able to style the splitter stuff at some point in the future, and ideally also document the actual tree of the konsole UI for reference. that would be cool i think

alright thats all bye
