---
permalink: /ffxiv-hotbar-tab-macro-generator
title: Hotbar Tabs Macro Generator for Final Fantasy XIV
title_md: Hotbar Tabs Macro Generator for <cite>Final Fantasy XIV</cite>
category: tools
stylesheets:
  - /interactive.css
style: |
    :root {
        --theme-light-text-color: hsla(360, 100%, 4%, 0.9);
        --theme-light-body-background:
            linear-gradient(50deg,  hsla(360,58.1%,88%,0.9), transparent 50%),
            linear-gradient(180deg, hsla(20,58.1%,88%,0.9), transparent 66%),
            linear-gradient(290deg, hsla(32,58.1%,88%,0.9), transparent 66%),
            white;
        --theme-dark-text-color: hsla(360, 100%, 97%, 0.9);
        --theme-dark-body-background:
            linear-gradient(50deg,  hsla(360,58.1%,12%,0.9), transparent 75%),
            linear-gradient(180deg, hsla(20,58.1%,12%,0.9), transparent 66%),
            linear-gradient(290deg, hsla(32,58.1%,12%,0.9), transparent 78%),
            black;
    }
    /* stupid hack */
    label + label {white-space: nowrap}
---
# Hotbar Tabs Generator

A little tool for making fancy tabbed HUD layouts in FFXIV.

{% include image.html
	src="/assets/xiv-hotbar-tabs/top.gif"
	alt="Screen recording of a tabbed hotbar interface in FFXIV. The first tab starts open; the second is opened, then the third, then an item is removed from the first and saved."
%}


<div id="app" class="box">
    <h2>Let's Generate You Some Macros</h2>
    <noscript>
        <p>This tool requires Javascript to run, sorry.</p>
        <style>#app form {display: none}</style>
    </noscript>
    <form id="params">
        <p><label>
            Number of tabs:
            <input type="number" name="tabs" value=3>
        </label></p>
        <p>
            Hotbars controlled by tabs (these must be shared):<br>
            <label><input type=checkbox name=hotbars value=1> 1</label>
            <label><input type=checkbox name=hotbars value=2> 2</label>
            <label><input type=checkbox name=hotbars value=3> 3</label>
            <label><input type=checkbox name=hotbars value=4> 4</label>
            <label><input type=checkbox name=hotbars value=5> 5</label>
            <label><input type=checkbox name=hotbars value=6> 6</label>
            <label><input type=checkbox name=hotbars value=7 checked> 7</label>
            <label><input type=checkbox name=hotbars value=8 checked> 8</label>
            <label><input type=checkbox name=hotbars value=9 checked> 9</label>
            <label><input type=checkbox name=hotbars value=10 checked> 10</label>
        </p>
        <details class="box">
            <summary>Advanced options...</summary>
            <p>
                <label>
                    Hotbar command:
                    <select name=hotbarcmd>
                        <option selected>/hotbar</option>
                        <option>/pvphotbar</option>
                        <option>/crosshotbar</option>
                        <option>/pvpcrosshotbar</option>
                    </select>
                </label>
            </p>
            <p>
                <label><input type=checkbox name=classjobs value=current> Make tab 1 job-dependent</label>
                <br><small>(disable saving to combat jobs if you use this; see <a href="#advanced-tips">caveats below</a>)</small>
            </p>
            <p>Classes/jobs for storing tabs:</p>
            <div style="padding-inline-start: 1.5rem">
                <p>
                    <em>Combat classes:</em> <button type=button onclick="toggleClassjobs('class')">Toggle All</button><br>
                    <label><input type=checkbox name=classjobs data-type="class" value=GLA checked> GLA</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=MRD checked> MRD</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=LNC checked> LNC</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=PGL checked> PGL</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=ARC checked> ARC</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=THM checked> THM</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=CNJ checked> CNJ</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=ACN checked> ACN</label>
                    <label><input type=checkbox name=classjobs data-type="class" value=ROG checked> ROG</label>
                </p>
                <p>
                    <em>Combat jobs:</em> <button type=button onclick="toggleClassjobs('job')">Toggle All</button><br>
                    <label><input type=checkbox name=classjobs data-type="job" value=PLD checked> PLD</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=WAR checked> WAR</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=DRG checked> DRG</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=MNK checked> MNK</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=BRD checked> BRD</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=BLM checked> BLM</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=WHM checked> WHM</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=SMN checked> SMN</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=SCH checked> SCH</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=NIN checked> NIN</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=DRK checked> DRK</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=MCH checked> MCH</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=AST checked> AST</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=SAM checked> SAM</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=RDM checked> RDM</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=BLU checked> BLU</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=GNB checked> GNB</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=DNC checked> DNC</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=RPR checked> RPR</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=SGE checked> SGE</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=VPR checked> VPR</label>
                    <label><input type=checkbox name=classjobs data-type="job" value=PCT checked> PCT</label>
                </p>
                <p><em>crafter/gatherers maybe eventually:tm:</em></p>
            </div>
        </details>
        <p><button>Generate</button></p>
    </form>
    <div id="output"></div>
</div>
<script>
    function generateTabMacros (command, classjobs, hotbars) {
        return classjobs.map((classjob, i) => ({
            open: hotbars.map(hotbar => `${command} copy ${classjob} ${hotbar} share ${hotbar}`).join('\n'),
            save: hotbars.map(hotbar => `${command} copy share ${hotbar} ${classjob} ${hotbar}`).join('\n'),
        }));
    }
    const form = document.getElementById('params');
    const output = document.getElementById('output');
    form.addEventListener('submit', event => {
        event.preventDefault();
        const data = new FormData(event.target);
        const tabCount = parseInt(data.get('tabs'), 10);
        const hotbars = data.getAll('hotbars');
        const classjobs = data.getAll('classjobs');
        const command = data.get('hotbarcmd');
        const macros = generateTabMacros(command, classjobs.slice(0, tabCount), hotbars);
        output.innerHTML = '<h2>Output</h2>';
        macros.forEach((tab, i) => {
            output.innerHTML += `
                <h3>Tab ${i + 1}</h3>
                <p>Open tab ${i + 1} <button onclick='navigator.clipboard.writeText(${JSON.stringify(tab.open)})'>Copy macro</button></p>
                <pre>${tab.open}</pre>
                <p>Save tab ${i + 1} <button onclick='navigator.clipboard.writeText(${JSON.stringify(tab.save)})'>Copy macro</button></p>
                <pre>${tab.save}</pre>
            `;
        });
    });
    /* advanced settings button helpers */
    function toggleClassjobs(type) {
        const inputs = document.querySelectorAll(`input[name=classjobs][data-type=${type}]`);
        if ([...inputs].every(input => input.checked)) {
            inputs.forEach(input => input.checked = false);
        } else {
            inputs.forEach(input => input.checked = true);
        }
    }
</script>

## How-To

- Fill in how many tabs you want.
- Select which hotbars will be controlled by the tabs. The tab buttons themselves will also live on one of these bars, so plan accordingly to make sure you have enough slots to fit everything you want.
- Click "Generate" and copy/paste the resulting macros into your macro list.
  - The "Open" macros display the specified tab on your hotbars.
  - The "Save" macros save the current layout of your hotbars into the specified tab.

After copying all your macros, you'll need to set up your layout for the first time.

- Make sure the selected hotbars are set to shared. This is done in Character configuration > Hotbars > Sharing.
  {% include image.html
      src="/assets/xiv-hotbar-tabs/sharing.png"
      alt="Screenshot of the sharing menu"
  %}
- Clear these hotbars and set up the layout for your tabs however you like, making sure each "Open" macro is added somewhere.
- In the "User Macros" window, go down the list of "Save" macros you copied, and run every single one in sequence (right-click > Execute on each). This will save your base layout to all your tabs.
  {% include image.html
      src="/assets/xiv-hotbar-tabs/setup-1.gif"
      alt="Screen recording of the &quot;Open&quot; macros being dragged from the macros window into a hotbar, and the &quot;Save&quot; macros being run in sequence afterwards"
  %}
- Try out each tab button. If you've done everything correctly, nothing should change when you click each tab. If the buttons disappear, you've done something wrong.
- At this point you're ready to customize the appearance of all your tabs. Press a tab button, customize however you like, and then run the corresponding "Save" macro for that tab.
  {% include image.html
      src="assets/xiv-hotbar-tabs/setup-2.gif"
      alt="Screen recording of a tab button being clicked, the tab's &quot;Open&quot; macro being dragged to replace the tab button, and several abilities being dragged into the tab. The save button is clicked, a second tab is opened, and the first is reopened to demonstrate that the changes were saved"
  %}

## How it Works & Caveats

Normally, hotbar contents are stored separately for each class/job. When you turn on sharing for a hotbar, that hotbar's contents come not from any specific class/job, but from a separate "shared" storage space independent of the others. The class-specific hotbar data still exists, and can be manipulated via the `/hotbar` command, but is inaccessible in the UI. These macros work by saving your tab layouts to these unused, invisible hotbar slots "underneath" the shared hotbar.

The hotbar you see on screen always corresponds to the "shared" hotbar state, while each tab you set up is stored in the hotbar state of a particular job or class. Opening a tab works by copying the corresponding class/job hotbar into the shared hotbar, and saving is just the opposite.

Additionally, since combat classes and jobs are distinct and *do not share hotbar slots with each other*, we can make the setup even less intrusive by storing the tabs in class (e.g. Marauder) hotbars rather than job (e.g. Warrior) hotbars. If you want more than nine tabs, however, you run out of classes, and the tool will begin storing further tabs in job hotbars. This is still inconsequential for most people and only causes problems if you tend to toggle your hotbars in and out of sharing mode frequently.


## Advanced Tips

- You can replace the "Open" button for the current tab with its "Save" macro instead; this will let you easily edit your tabs without having to open the macros menu, and also lets you pick a different icon to use when the tab is selected.
  - The light/dark numbered macro icons make good candidates for contrasting active/inactive tab icons!
- Adding a "close" button is easy; it's just an additional tab that you don't add anything to after initial setup. You can hide the "close" button when no other tabs are open by just removing it from the "empty" tab.
- There's nothing that actually requires you to have all your tab-switching buttons be visible at all times. Since the tab switching buttons themselves are stored in each individual tab, It's possible to nest tabs or do even fancier layouts with some additional planning. These cases often benefit from either making empty hotbar slots transparent, or modifying some of the macros to show/hide different hotbar UI elements.
- If you want to get *really* fancy, you can also have one tab that's job-dependent (behaving like a non-shared hotbar, with different contents for each job). For one of your tab's macros, rather than using a specific class like `MRD`, you can use the keyword `current`. This will cause that tab to be loaded from/saved to your current job's hotbar. This also limits you to nine other tabs, since this uses all your job slots and you only have the base classes left to store other tabs in.
