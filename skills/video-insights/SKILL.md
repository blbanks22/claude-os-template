---
name: video-insights
description: Use this skill whenever a user wants to extract a transcript, summarize, or pull insights from a video (YouTube or other platforms). Triggers include "/video-insights <url>", "summarize this video", "transcribe this", "what does this video say", "pull insights from this video", "give me the TL;DR of this video", or when a user pastes a YouTube/video URL and asks for analysis. Fetches the transcript via YouTube's timedtext API, page HTML, or yt-dlp, then produces a structured insight summary (TL;DR, key takeaways, quotes, action items).
---

# video-insights

Extract a transcript from a video URL and surface key insights.

## Trigger

Invoked with `/video-insights <url>` or when the user asks to summarize, transcribe, or extract insights from a video.

## Steps

### 1. Parse the URL

Identify the platform and extract the video ID:

- **YouTube** (`youtube.com/watch?v=ID` or `youtu.be/ID`): extract the `v=` param or path segment.
- **Other platforms**: note the full URL, transcript extraction may not be available.

### 2. Fetch the transcript

Try these methods in order, stopping at the first that succeeds.

#### Method A: YouTube timedtext API (fastest, no auth)

Fetch:
```
https://www.youtube.com/api/timedtext?lang=en&v=VIDEO_ID&fmt=json3
```

If that returns empty, also try:
```
https://www.youtube.com/api/timedtext?lang=en-US&v=VIDEO_ID&fmt=json3
```
```
https://www.youtube.com/api/timedtext?lang=en&v=VIDEO_ID
```

Parse the response:
- `fmt=json3`: extract `.events[].segs[].utf8` text fields, joined in order.
- XML fallback: extract text from `<text>` tags, HTML-decode entities.

#### Method B: Extract from YouTube page HTML

Fetch `https://www.youtube.com/watch?v=VIDEO_ID` and look for:
- A JSON blob containing `"captionTracks"`, extract the `baseUrl` from the first English track and fetch it.
- Parse XML `<text>` elements from that URL.

#### Method C: yt-dlp (if installed)

```bash
yt-dlp --write-auto-subs --sub-lang en --skip-download --sub-format vtt -o "/tmp/vt_%(id)s" "URL"
cat /tmp/vt_VIDEO_ID.en.vtt 2>/dev/null || cat /tmp/vt_VIDEO_ID.en-orig.vtt 2>/dev/null
```

Parse VTT: strip timestamp lines (`\d\d:\d\d.*-->.*`), deduplicate adjacent repeated lines, join.

#### If no transcript is available

Tell the user clearly. Offer to analyze the video title/description if they paste metadata, or suggest installing `yt-dlp` via `brew install yt-dlp` for broader support.

### 3. Clean the transcript

- Remove `[Music]`, `[Applause]`, `[Laughter]` and similar filler tags.
- Collapse duplicate lines that appear from rolling captions.
- Join into readable paragraphs (split on long pauses > 3s where timestamp data is available).

### 4. Extract insights

Analyze the cleaned transcript and produce a structured output:

```
## Video Insights

**Source:** <title or URL>
**Length:** ~X minutes of transcript

### TL;DR
2–3 sentence summary of the core message.

### Key Takeaways
- Bulleted list of the most important points (5–10 bullets).

### Supporting Details
For each key takeaway that has nuance or data behind it, expand with 1–2 sentences.

### Notable Quotes
2–4 direct quotes worth saving verbatim (with approximate timestamp if available).

### Action Items / Next Steps
If the video contains recommendations, frameworks, or calls to action, list them here.

### Gaps / Caveats
Flag anything unsubstantiated, speculative, or that warrants verification.
```

Tailor depth to video length:
- < 10 min: TL;DR + Key Takeaways only unless asked for more.
- 10–60 min: full structure above.
- > 60 min: full structure + a "Chapter Breakdown" section summarizing major segments.

### 5. Offer follow-up options

End with a short prompt like:
> Want me to go deeper on any section, pull specific quotes, or export this as a markdown file?
