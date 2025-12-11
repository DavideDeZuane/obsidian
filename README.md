In this section there are the guidelines to write inside the wiki.


## Shortcuts

- `Alt+t`: change theme

## Tags
Each tags is an empty notes. 
To apply the tag to a note, add the link to the notes in the metadata filed of the notes (the link is usual syntax, "[[]]"). For example:
```
{{TITLE}}
Tags: [[example_tags]]
```

## Indexes
We can use a tags as index, a former tag.
Inside this note we can add all the notes that belong to this category. 

## Images
To include a **draw.io** graph inside a notes:
1. Create a `new diagram` then edit the notes
2. Create the diagram with `drawio` editor
3. Use `![[some_dir/some_name.svg]]` to display your figure in the note.

To center an image, we have to modify the `css` of obsidian. So must follow the following procedure:
1. Create a `css` file inside `.obsidian/snippets`
2. Paste the following code
```css
img[alt*="center"] {
    display: block;
    margin-left: auto;
    margin-right: auto;    
}
```
3. Go in `settings->appearence` and reload the CSS Snippets option
4. After that enable the button for the file created

To apply the change use the following syntax 
```
![[image | center | size]]
```
