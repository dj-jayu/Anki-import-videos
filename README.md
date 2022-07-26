This addon is an modified anki addon to import images and videos as flashcards in Anki.

The modification imports the videos as embeded html elements.

Meaning the videos will be played in the card itself, and not in the external video player.

This way, the video won't close after playing, and we can use javascript and html to control the speed, play, pause and autoloop the video.

The videos that will be imported need to be in the '.webm' format, so the addon can create a card with the video embedded in HTML (anki doesn't like mp4
embeded videos for some reason).

Anki documentation for addons is pretty bad, so I couldn't understand everything in the original code, but it was enough to do the modifications
I needed.

[Link to original add-on at ankiweb](https://ankiweb.net/shared/info/1531997860)

[Github of the original addon](https://github.com/hssm/media-import)

I haven't published the addon in the anki website yet.

So you will need to download the raw files and create an addon.

I will explain how to do this in the future.

------------------------------------------------------------------------------------------------------------------------------------------------------------
I use the below shortcuts in my cards:
| key | action |
|-----|--------|
| "`" | play/pause |
| "q" | slower |
| "w" | faster |
| "z" | backward 3 seconds |
| "x" | forward 3 seconds |

To apply this settings go to "Cards" -> "Templates" and paste the following code:
```html
<h1>{{Tags}}</h1>
{{Front}}

<p>
  
</p>
<script>
	const execute = function(e) {
        document.querySelector('p').textContent = e.key;        		

        if (e.key === "w") {
            document.querySelector('video').playbackRate += 0.25;
            document.querySelector("p").textContent = document.querySelector("video").playbackRate.toFixed(2) + "x";
        }
        if (e.key === "q") {
            document.querySelector('video').playbackRate -= 0.25;
            document.querySelector("p").textContent = document.querySelector("video").playbackRate.toFixed(2) + "x";
        }
        if (e.key === "z") {
            document.querySelector('video').currentTime -= 3;
        }
        if (e.key === "x") {
            document.querySelector('video').currentTime += 3;
        }
        if (e.key === "`") {
            if (document.querySelector('video').paused) {
            document.querySelector('video').play();
        }
        else {
            document.querySelector('video').pause();
        } 
    }
}
               
    document.addEventListener("keypress",execute);
</script>
```

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
Original description:

This add-on will allow you to import media files into your Anki collection and use their file names as a component of the note. You can create cards that might look like this (using *apple.jpg*):

![Card](https://raw.githubusercontent.com/hssm/media-import/master/docs/card.png)

When the add-on is installed, a `Media Import...` option will be added to the `Tools` menu.

![Menu](https://raw.githubusercontent.com/hssm/media-import/master/docs/menu.png)

Selecting this menu item will open the Media Import window.

![Dialog](https://raw.githubusercontent.com/hssm/media-import/master/docs/dialog.png)

From this window, you are able to:
- Browse and select which folder to use as the source of media files
- Choose which note type to use for the imported notes
- Decide what content to put into each of the fields
 
Here is a list of the content available to insert into fields. We will use an example file named `apple.jpg`.
 - Media - The media file itself (image or audio will appear on the card)
 - File Name - The name of the file without the extension (*apple*)
 - File Name (full) - The name of the file including the extention (*apple.jpg*)
 - Extension - Only the extension of the file (*jpg*)
 - Sequence - A number indicating the order in which the file was imported. If 15 files were imported, each file will contain a value starting from 0 to 14.




All new generated cards are added to a deck named `MediaImport`. This deck is created for you automatically if it doesn't exist.

![Complete](https://raw.githubusercontent.com/hssm/media-import/master/docs/complete.png)
