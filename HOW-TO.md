# Shelf TV: your iPad as the TV, your iPhone as the remote

`index.html` is a single page with two modes:
- **TV mode** (`…/index.html?tv`) runs full screen on the iPad and shows whatever your phone picks.
- **Remote mode** (`…/index.html`) runs on your iPhone. You search movies and shows with posters, tap an episode, and it opens on the TV in your FMHY site's player.

There's no Stremio, no DNS profile and no account. The phone and iPad talk over a direct connection on your Wi-Fi (WebRTC). The free PeerJS server is only used to find each other by your 8-character pairing code.

## 1. Put the page online (5 minutes, on the Mac)
Safari needs to load it from an https address. The free way is GitHub Pages:
1. Sign in at github.com and create a new **public** repository called `shelftv`.
2. Choose **Add file > Upload files** and drop in `index.html` and `peerjs.min.js`.
3. Go to **Settings > Pages**, set Source to **Deploy from a branch**, then choose **main** and **/(root)**, and save.
4. About a minute later the page is live at `https://YOURNAME.github.io/shelftv/`.

(If you connect GitHub to this project, I can do this step for you.)

## 2. iPad (the TV)
1. Open `https://YOURNAME.github.io/shelftv/?tv` in Safari, then tap **Share > Add to Home Screen**.
2. **Settings > Display & Brightness > Auto-Lock > Never.** Keep the iPad charging through the hub.
3. **Fill the monitor:** turn on Stage Manager (Control Center). Drag Shelf TV onto the external display and make it full screen. Without Stage Manager, the iPad mirrors its own screen with black bars.
4. **Sound:** Control Center > AirPlay audio > your Bluetooth speaker or AirPods (the monitor has no speakers).
5. Open Shelf TV from the Home Screen and tap **Tap to start**. That one tap is only needed after a restart.
6. Optional: **Settings > Accessibility > Guided Access**, then triple-click the top button to lock the iPad into Shelf TV.

## 3. iPhone (the remote)
1. Open `https://YOURNAME.github.io/shelftv/` in Safari, then tap **Share > Add to Home Screen**.
2. Settings opens. Type the **pairing code** from the corner of the TV screen.
3. **Add your sites.** For each site, open it in Safari, start *Dune: Part Two* and copy the watch-page address. Then open any *Breaking Bad* episode other than S1 E1 and copy that address too. Paste them under **Add a site** (one is enough if the site only has movies or only shows). The remote shows the pattern it learned, such as `…/movie/{tmdb}`. Add as many sites as you like: Movy, Cinejoy, Rive, whatever FMHY lists.
4. Now search, tap a poster, and tap **Play on TV** or an episode. If you've saved more than one site, a row of site buttons appears above **Play**. Tap one to switch, for example when Movy is down or missing a title. The last one you picked becomes the default. You can change or remove sites anytime under **Settings**.

## Ad-free direct playback (recommended)
Instead of loading a website, the iPad fetches the video file from a free source and plays it in Shelf TV's own player. There are no ads or pop-ups, and the remote gets ⏯, ↺10, 30↻, a seek bar, ⇄ (switch source) and ⏻. Shows auto-play the next episode, and movies resume where you left off.

One-time setup on the phone: open **pengu.uk** in Safari (PenguPlay, free HTTP streams, no account). Configure it if you want, then copy its install link (it starts with `stremio://` or ends in `/manifest.json`). In Shelf TV, go to **Settings > Ad-free sources**, paste the link and tap **Save sources**. From then on, **Play on TV** plays ad-free, and the site buttons on each title let you fall back to a website.

If a title won't play, tap **⇄** and try another source. Files in formats Safari can't play (such as some .mkv files) are skipped automatically.

## Any website at all: "Send to TV"
For sites that don't fit the pattern trick (sports, live TV, YouTube, anything else):
- **Paste a link** into **Send any link** on the remote's home screen, **or**
- **Set up a one-time Share-sheet shortcut** in the Shortcuts app:
  1. Tap **+** and name the shortcut **Send to TV**. Under its settings (ⓘ), turn on **Show in Share Sheet**.
  2. Add the action **URL Encode** and set it to encode **Shortcut Input**.
  3. Add the action **Open URLs** and type `https://YOURNAME.github.io/shelftv/?send=`. Right after that text, insert the **URL Encoded Text** variable.
  Then, in Safari on your phone, browse any site, open the movie's page, and tap **Share > Send to TV**. It opens on the monitor.

**Remote buttons:** **Home** goes back to the TV home screen. **Reload** reloads the player. **Page** opens the site on its own, without Shelf TV around it, if the site refuses to play inside Shelf TV (the remote stops working until you reopen Shelf TV). **Off/On** blanks the screen and stops the video.

**Pause and volume:** on the iPhone, go to **Settings > Accessibility > Control Nearby Devices** and pick the iPad. That gives you play/pause and volume for any site's video. Add it to Control Center for one-tap access.

**Pop-ups:** "Block pop-ups and redirects" (on by default) stops the site from opening ad tabs or redirecting away. Some sites detect this and refuse to play. If yours does, untick it, and consider the free uBlock Origin Lite app for Safari on the iPad.

## Things I couldn't test from here
- Whether your site allows being shown inside another page. Some sites block it, and you'd see a blank or "refused to connect" screen. If so, try another FMHY site from the same list, or use **Page**.
- Whether your site starts playing by itself. If it waits for you to tap its play button, nothing on the phone can tap it for you. Sites that autoplay or use "Auto-Next" work best.
- Catalog and posters come from Stremio's free public catalog (Cinemeta). You don't need the Stremio app.

Tested: both pages in Chromium with a mock relay, catalog and sites: pairing, learning the link pattern, two saved sites and switching between them, movie and episode playback, Send to TV links, Home, Off/On and recently watched.
