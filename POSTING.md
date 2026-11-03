# How the daily recap is posted to Instagram

Account: @steadyinvestor.sg only (IG user id 17841477711587846). Ken approved posting daily recaps with no per-post approval.

1. Copy the day's videos into this repo as `videos/<YYYY-MM-DD>/recap-en.mp4` and `recap-zh.mp4`, then commit and push to `main`.
2. Public URL: `https://raw.githubusercontent.com/HuangTaooooo/steadyinvestor/main/videos/<YYYY-MM-DD>/recap-<lang>.mp4`
3. With Zapier Instagram for Business "Make API Mutating Request":
   POST `https://graph.facebook.com/v19.0/17841477711587846/media` with query `media_type=REELS`, `video_url=<url>`, `caption=<caption>`, `share_to_feed=true`.
4. Poll GET `https://graph.facebook.com/v19.0/<container id>?fields=status_code` until `FINISHED` (it takes a few minutes).
5. POST `https://graph.facebook.com/v19.0/17841477711587846/media_publish` with query `creation_id=<container id>`.
6. Read back the permalink: GET `/<media id>?fields=permalink`.

Each Zapier call uses 2 Zapier tasks.
