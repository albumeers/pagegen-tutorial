Tutorial
================

This tutorial is designed to help you learn the process of building an album page and some of the common constructs used in the album files.  The file "tutorial-complete.xml" is available as a completed file that can be used to help show the concepts as a completed file.  The examples used are taken from actual album pages but are meant simply as a tutorial.

Before You Begin
----------------

* Download and Execute the stamp-pagegen tool from [www.drakeserver.com](http://www.drakeserver.com www.drakeserver.com) to ensure there are no issues running the tool.  Depending on your operating system a desktop icon/application group may be installed you can use for further access of the tool.
* Download the starter-template.xml and tutorial-complete.xml from the list above.  (you can also get them by clicking the "Download ZIP" on the right side.  (If using the ZIP file expand it using a tool from your computer (Windows can open the file in explorer) and copy the contents to a directory on your disk.
* Open the Stamp Album Generator (stamp-pagegen) tool and leave this open.  Set the Configuration drop-down to "Letter Standard (8.5" x 11.0")"
* Open a text or xml editor [XML Copy Editor](http://xml-copy-editor.sourceforge.net/) works well for many (you may want to choose/configure a less annoying font - go to Tools->Options menu and select "Editor" tab and change the "Font" value.
* Open a web-browser tab and point it to http://www.drakeserver.com/dtds/pagegen.dtd - you will find this invaluable as your learn the syntax more.

Authoring Your First Page
-------------------------
 
Switch to the Stamp Album Generator tool 
1. in the "Input File" select the "starter-template.xml" from the folder you selected.
2. in the "Output Folder" choose a generation folder (it could be where you copied the xml files to - it just needs to be writable)
3. click "Generate" button.  

<img src="images/click-generate.png" width="400px"></img>

You should get an error like this:

<img src="images/No-page-error.png" width="400px"></img>

This means you are ready to author your first page.  Notice the "Open ..." button is disabled (this is because the PDF does not exist).

4. Switch to the text editor (using ALT-TAB or other method) and between the <album> </album> tags add a <page> tag with a title attribute like this:

```XML
	<page title="My First Page">
	
	</page>
```

5. Save the file in the editor and switch back to the Stamp Album Generator and click "Generate...".  
6. Now the "Open..." button should be enabled.  Click it (Note: This requires you to have a valid PDF reader installed and configured for your system like Adobe PDF Reader) - the Album should open up, have a single page that says "My First Page".

_Some Obversations_
* Notice the title is in ALL CAPS. This is simply part of the definition/generation and it is converting it to upper case.
* If you close the PDF select the "Render Page Borders" and regenerate follow by opening the PDF you'll notice the title is centered "between" the borders.  This was all calculated automatically for you.

Creating a Set of Stamps
------------------------

In this tutorial we will add to the current file and add another page that contains a set of four stamps and a souvenir sheet.  

To begin switch back to the text editor
1. Add a new page similiar to what you did previously directly after the &lt;/page&gt; tag on a new line.  Set the name to "Japan"
2. Write the closing page tag &lt;/page&gt; on a new line and add a blank line between them. 

*HINT* This is a good practice.  Create your start and ending tags first then fill in the content.  Also try and use TABs to intend your document at each level of the structure.  It makes it easier to read.

Now we are going to create a set of stamps.  The &lt;set&gt; are the children (one of) a &lt;page&gt; element.  Sets have a series of optional attributes and children elements that we will define in this step.

3. Create a &lt;set&gt; tag and provide it an issue of "1959" and a description of "Wedding of Crown Prince Akihito and Princess Michiko".  Close the tag on a new line leaving an empty line between (some editors will do this automatically when you hit "ENTER" after typing the &gt; character).  Here is what you should have.

```XML
  <set issue="1959" descripton="Wedding of Crown Prince Akihito and Princess Michiko">
  
  </set>
```

4. Save the xml file and switch back to the generator and generate.  You should see the JAPAN title plus 1959 in a larger text followed by the description all centered.
5. Switch back to the text file and we are going to add a row for stamps.  The &lt;row-set&gt; is a construct that allows us to have a set of stamps (the &lt;s&gt; tag) or define set-tenant blocks (with the &lt;set-tenant&gt; tag).  Row-sets can have a description, define custom horizontal spacing (not used often) and specify a vertical alignment attribute "valign" which is useful when you have mixed sized stamps.  Lets create a row-set that has a description "Perforated 13½"  Notice the ½ character.  A few of these characters, can be used (or encouraged) including (¼½¾£) but many non-Latin-1 characters will not render in the PDF and should be avoided.

```XML  
  <set issue="1959" descripton="Wedding of Crown Prince Akihito and Princess Michiko">
	<row-set description="Perforated 13½">
	
	</row-set>
  </set>
```

6. Now we are going to add three stamp boxes.  Boxes are defined using the &lt;s&gt; tag and include a few attributes (such as image and shape).  However for 99% of the stamp boxes they are empty "s" tags with string content.  The content is a little querky to learn (but once learned it is straight forward).  All "s" tags require _five_ sets of "" four of which may or may not have content.  There are as follows:
   * The first set of "" represents the stamp dimensions as "width height".  This is in mm, and is the measurement of the stamp frame + any paper to the perforations.  ie. it is the paper size (not image size).  The system will automatically generate extra width and height to give it a centered appearance and allow for things like stamp mounts.
   * The second set of "" represents the rate/denomination.  A blank line will be added after it automatically.  Examples include "1c" or "£5"
   * The third set of "" represents the primary description.  This is used to describe the color of the stamp such as "Red and Green".  For modern stamps with many colors, "Multicolored" is used.
   * The fourth set of "" is often empty on early stamps unless it is calling out a specific feature eg. "(Thick Paper)".  For modern stamps it is used to describe the stamp in brackets "(Pugg Dog)".  This descriptor gets a unique font declaration and is often italicized.  Text generally should be included in parenthesis ().  On earlier issues this is often used to call out a specific variant where a unique row-set is not desired.
   * The fifth set of "" is used for catalogue numbers.  Typically the common number is shown first followed optionally by a more specialized number. In the example below, "667" is refering to Scott #667 and (798) represents Stanley Gibbons #798 

Lets add three boxes to the stamp-row as follows:

```XML  
  <set issue="1959" descripton="Wedding of Crown Prince Akihito and Princess Michiko">
	<row-set description="Perforated 13½">
		<s>"37 26" "5y" "Bluish Violet and Reddish Purple" "" "667 (798)"</s>
        <s>"37 26" "10y" "Maroon and Brown" "" "668 (799)"</s>
        <s>"37 26" "20y" "Sepia and Orange-Brown" "" "669 (800)"</s>
	</row-set>
  </set>
```

7. Save the file and switch back to the Album Generator Tool and hit Generate (make sure the PDF is not open).  Open the PDF if successful and look at the output.  You should see something like this:

<img src="images/Japan-firstrow.png" width="500px"></img>





