# TextCommentryTest

## Overview

This is a test for applying comments which link to specific regions of text within a formatted document (html). A working sample can be found [here](http://ivodonev.github.io/TextCommentryTest/). 

The page loads with some gibberish on the left and 3 previously saved comments. Selecting any text and clicking "add comment" triggers a popup where you enter a message and save your comment. Clicking on a comment on the right will highlight the appropriate region.

## General Approach

Bootstrap is used for general styling and is used to split the view in two using cols. On smaller devices the comments appear underneath. An angular app is used to manage data binding although this may be considered overkill for this scenario. We load the data which consists of a url for the "html" to display in the left column and the list of comments and their appropriate highlighted sections. 

The [rangy](https://github.com/timdown/rangy) library was used for saving and restoring selections. I found the basic save and restore selection mechanism of the library was insufficient as it did not work across page reloads or minor runtime changes to the dom (which occur all the time in angular and other SPA frameworks). I ended up using the highlighter module from rangy which is based on character offsets and is more robust in this sense although it is [slower](https://github.com/timdown/rangy/wiki/Highlighter-Module). The highlighted sections are saved as strings using the `serialize` method for the highlighter module in rangy.


I have also used the [angular-bootstrap ui](https://angular-ui.github.io/bootstrap/) library as a wrapper for modal dialogs. Again this is a very large library for a very small section of functionality but I find the restriction of scope provided by these modal dialogs provides a clean linear approach to modal pops.

## Shortcomings and Prospective

Currently the implementation is rather bloated but various components such as angular and bootstrap could be removed. 

Also currently the text is inserted directly into the dom - which can be dangerous. Preferably a frame should be loaded with the text within - I chose not to do this at this stage as I would have to inject additional styles for the highlighting into the frame.

A nice additional feature would be to automatically scroll to the location of the comment upon clicking it.

More importantly the comments cannot update with updates to the text. Since they are based on regions of the document any changes will result in either they not working or referencing the incorrect regions. An approach based on anchors embedded directly into the text may be more robust.


