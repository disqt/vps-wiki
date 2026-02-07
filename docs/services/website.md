# Disqt Website

- **Repository**: [disqt-info-website](https://github.com/disqt/disqt-info-website)
- **URL**: [disqt.com](https://disqt.com)

## Overview

A static HTML/JS/CSS dashboard that displays the live status of all game servers. The site features a neon/cyberpunk visual theme.

## Features

- **Real-time status**: Fetches server data from the `/servers` API endpoint (provided by [lgsm-info-api](lgsm-info-api.md))
- **Player counts**: Shows current and maximum players for each server
- **Click-to-copy**: Server addresses can be copied to clipboard with a single click

## Hosting

The website is served directly by nginx as static files. There is no build step required -- the HTML, CSS, and JavaScript files are served as-is.

## Deployment

Update the static files on the server and nginx will serve the new version immediately. No restart is needed.
