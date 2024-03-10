# Google Chat Takeout Reader

## Introduction

Some time in mid to late 2023, Google ceased Takeout support for **Hangouts** and converted it to **Google Chat**. In that transition, the format of the JSON output files changed as well.

This repo contains a simple, client-side reader for Google Chat Takeout JSON files.

## Notes
This is a pure javascript utility. Nothing is uploaded to the internet. It all runs on your local machine.

## How to use the Google Chat Takeout Reader
You can use the hosted version of this utility by clicking here: https://mrwoof.github.io/google-chat-takeout-reader/google_chat_takeout_reader.html

**- OR -**

If you'd prefer to download it the utility and load it into your browser locally, do the following:

- Download the file `google_chat_takeout_reader.html`
    - And of course `static/img/chat-reader-logo.png` so you don't have ae broken imnage in the header
- Open that file in Google Chrome
- Select the directory containing your _uncompressed_ Google Chat Takeout files (this won't work on `.zip` or `.tgz` files -- you need to unzip them first)
- See your chats

That's it!


## Technical Notes
- This code only works with Google Chrome to my knowledge, due to its use of `window.showDirectoryPicker` -- not all browsers support directory selection.
- This code was only tested on MacOS.
- Uses Bootstrap 5.3.0 and jquery 3.6.0, sourced from public URLs

## Acknowledgements
Shout out to the project **Hangouts Reader** at https://github.com/Jessecar96/hangouts-reader/. I had previously used this utility and had modified it locally. I was going to contribute to it, but when Google completely changed the JSON structure, I wrote a new one from scratch.

## PRs welcome
Though I can't promise quick turnaround on reviews...


_-- Michael Richman_
