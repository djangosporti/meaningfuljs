<link rel="stylesheet" href="meaningful.css"/>Use-cases
=====================================

Small database/knowledgebase
----------------------------

Sometimes people make things more complex to find good solution for it. This becomes evident if you will realize million people have structured information in their heads, then they create web pages, where this information and its structure flattened by HTML, and then they look for good search engines to find this information afterwards. Yes, all this that's simple: the main problem is not in good algorithm for search engine but in the fact that we lose structure of information when we flatten it with HTML or any other format (even plain text).

Look at this HTML:

```
<table meaning="planet">
	<thead meaning="planet [has property]">
		<tr>
			<th meaning="planet [has id]">Name</th>
			<th>Diameter</th>
			...
		</tr>
	</thead>
	<tbody meaning="[is instance of] planet">
		<tr>
			<td>Mercury</td>
			<td>4,878 km</td>
			...
		</tr>
		...
	</tbody>
</table>
```

Look at meaningful markup which is the result of such html:

<div class="meaningful">
Mercury <span class="rel">[has property]</span> diameter <span class="rel">[has value]</span> 4,878 km
</div>

And look on question which will give the correct answer:

<div class="meaningful-question">
What <span class="rel">[_] [is value of]</span> diameter <span class="rel">[of]</span> Mercury
</div>

Isn't that simple? Yes, of course, I know contemporary search engines already can answer such questions. But it concerns only very general facts. Try to ask them `When did solar eclipse occur the last time in my country?` even if you register related information in a web page.

Meaningful markup gives more possibilities and necessities:
* Meaning awareness (knowledge what meaning is and how to use it) should be widely accepted.
* Each piece of information should be tested with possible questions, which other people may ask.
* Provided answers should be considered not only for browsers but for other applications too.

Application ecosystem
---------------------

Imagine we have OS_like_OS operating system, which has UI with following components, interactions, and relations between them:

1. Mouse right click on the desktop or Properties key press causes a context menu to appear.
2. The context menu has Properties item which causes Desktop properties dialog to appear.
3. Desktop properties dialog has Appearance tab, which has color input, and which can cause a color picker to appear.
4. The color picker may change the desktop color.
5. /etc/ui.cfg is a configuration file, which has "desktop" section, which has "color", "pattern" values, which may change the desktop color and pattern respectively.
6. If "color-enabled" attribute in "desktop" section of /etc/ui.cfg is present then Appearance tab in Desktop properties dialog is visible/enabled.
7. Desktop appearance is defined by the desktop color, pattern, and picture.

As you may guess all this can be described with simplified markup:

<div class="meaningful">
<div>OS_like_OS desktop <span class="rel">[is property of]</span> mouse right click <span class="rel">[causes]</span> context menu</div>
<div>Properties key press <span class="rel">[causes]</span> context menu</div>
<br/>
<div>context menu <span class="rel">[has]</span> Properties item <span class="rel">[causes]</span> Desktop properties dialog</div>
<div>Desktop color picker <span class="rel">[causes]</span> Desktop color</div>
<br/>
<div>/etc/ui.cfg <span class="rel">[has part]</span> desktop section <span class="rel">[has property]</span> color attribute <span class="rel">[causes]</span> Desktop color</div>
<div>/etc/ui.cfg <span class="rel">[has part]</span> desktop section <span class="rel">[has property]</span> color attribute <span class="rel">[causes]</span> Desktop color</div>
<div>/etc/ui.cfg <span class="rel">[has part]</span> desktop section <span class="rel">[has property]</span> pattern attribute <span class="rel">[causes]</span> Desktop pattern</div>
<div>/etc/ui.cfg <span class="rel">[has part]</span> desktop section <span class="rel">[has property]</span> color-enabled attribute <span class="rel">[is condition of]</span></div>
<div class="indent">Desktop properties dialog Appearance tab </div>
<br/>
<div>Desktop properties dialog Appearance tab <span class="rel">[is the same]</span></div>
<div class="indent"><span class="rel">[/]</span> Desktop properties dialog <span class="rel">[has]</span> Appearance tab <span class="rel">[/#1]</span></div>
<div>OS_like_OS desktop <span class="rel">[is the same]</span></div>
<div class="indent"><span class="rel">[/]</span> OS_like_OS <span class="rel">[has]</span> desktop <span class="rel">[/#1]</span></div>
<div>Desktop color picker <span class="rel">[is the same]</span></div>
<div class="indent"><span class="rel">[/]</span> Desktop properties dialog Appearance tab <span class="rel">[has]</span> color input <span class="rel">[causes]</span> color picker <span class="rel">[/#2]</span></div>
<div>Desktop color <span class="rel">[is the same]</span></div>
<div class="indent"><span class="rel">[/]</span> OS_like_OS desktop <span class="rel">[has property]</span> color <span class="rel">[/#3]</span></div>
<div>Desktop pattern <span class="rel">[is the same]</span></div>
<div class="indent"><span class="rel">[/]</span> OS_like_OS desktop <span class="rel">[has property]</span> pattern <span class="rel">[/#4]</span></div>
<div>Desktop appearance <span class="rel">[is the same]</span></div>
<div class="indent"><span class="rel">[/]</span> Desktop color <span class="rel">[and]</span> Desktop pattern <span class="rel">[and]</span> Desktop picture <span class="rel">[/#5]</span></div>
</div>

Now we can ask some questions (it should be read as `How to change desktop color?`):

<div class="meaningful-question">
how <span class="rel">[_ @cause]</span> Desktop color
</div>

And answer, which should be read as:
* `Click mouse right click or press Properties key to make a context menu appear.` 
* `Then choose Properties item, which causes Desktop propeties dialog to be displayed.`
* `In that dialog click on Appearance tab (if color-enabled attribute in desktop section of /etc/ui.cfg is present).`
* `Then use color input to open color picker.` 

or 

* `Change color attribute in desktop section of /etc/ui.cfg`

<div class="meaningful">
<div>[</div>
<div class="indent">[</div>
<div class="indent2">[ 'mouse right click', '<span class="rel">[causes]</span>', 'context menu' ],</div>
<div class="indent2">[ 'Properties key press', '<span class="rel">[causes]</span>', 'context menu'],</div>
<div class="indent2">'context menu', '<span class="rel">[has]</span>',</div>
<div class="indent2">'Properties item', '<span class="rel">[causes]</span>',</div>
<div class="indent2">'Desktop properties dialog', '<span class="rel">[has]</span>',</div>
<div class="indent2">'Appearance tab', ['<span class="rel">[has condition]</span>', '/etc/ui.cfg', '<span class="rel">[has part]</span>', 'desktop section',</div>
<div class="indent3">'<span class="rel">[has property]</span>', 'color-enabled attribute' ],</div>
<div class="indent2">'[has]',</div>
<div class="indent2">'color input', '<span class="rel">[causes]</span>',</div> 
<div class="indent2">'color picker'</div>
<div class="indent">],</div>
<div class="indent">[ '/etc/ui.cfg', '<span class="rel">[has part]</span>', 'desktop section', '<span class="rel">[has property]</span>', 'color attribute' ]</div>
<div>]</div>
</div>

`How to change desktop appearance?`:
		
<div class="meaningful-question">
how <span class="rel">[_ @cause]</span> Desktop appearance
</div>

And answer only for configuration files (UI variants omitted for brevity):

<div class="meaningful">
<div>[</div>
<div class="indent">[ '/etc/ui.cfg', '<span class="rel">[has part]</span>', 'desktop section', '<span class="rel">[has property]</span>', 'color attribute' ],</div>
<div class="indent">[ '/etc/ui.cfg', '<span class="rel">[has part]</span>', 'desktop section', '<span class="rel">[has property]</span>',	'pattern attribute' ]</div>
<div>]</div>
</div>

In general, what you see is how documentation should work when it is not just a pile of documents but a complex of object-action-condition-cause-effect-relations. Of course, examples from above are quite simple but the next step of query could be `How to change desktop appearance if I upgraded OS_like_OS to 0.3 version?`, etc.