# Google Chat Takeout Reader

## Introduction

This repo contains a simple, client-side reader for Google Chat Takeout JSON files.

This is a pure javascript utility. Nothing is uploaded to the internet. It all runs on your local machine.

## How to use the Google Chat Takeout Reader

### Step 1
Download and unzip Google Chat files from Google Takeout at https://takeout.google.com/.

### Step 2

Use the **Google Chat Takeout Reader** to view them.

You can use the hosted version of this utility by clicking here: https://mrwoof.github.io/google-chat-takeout-reader/google_chat_takeout_reader.html

**- OR -**

If you'd prefer to download the utility and load it into your browser locally, do the following:

- Download the file <a href="https://raw.githubusercontent.com/mrwoof/google-chat-takeout-reader/main/google_chat_takeout_reader.html" target="_blank">`google_chat_takeout_reader.html`</a>
    - And of course download <a href="https://github.com/mrwoof/google-chat-takeout-reader/blob/main/static/img/chat-reader-logo.png" target="_blank">`static/img/chat-reader-logo.png`</a> so you don't have a broken image in the header
- Open that file in Google Chrome
- Select the directory containing your _uncompressed_ Google Chat Takeout files (this won't work on `.zip` or `.tgz` files -- you need to unzip them first)
- Grant permission for your browser to view the files on the file system
- See your chats

That's it!


## Technical Notes
- To my knowledge, this code only works with Google Chrome due to its use of `window.showDirectoryPicker()` -- not all browsers support directory selection.
- This code was only tested on MacOS.
- Uses Bootstrap 5.3.0 and jquery 3.6.0, sourced from public URLs

## Acknowledgements

Shout out to the project **Hangouts Reader** at https://github.com/Jessecar96/hangouts-reader/. 

I was going to contribute enhancements to that project, but Google changed the JSON structure of Takeout files when they transitioned from **Hangouts** to **Google Chat**, I wrote a new reader from scratch which is what is contained in this repo.

## PRs welcome

Though I can't promise quick turnaround on reviews...

<br>

Enjoy!

_-- Michael Richman_
