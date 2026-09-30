# 🌦️ Crow Weather Card

A weather card for [Home Assistant](https://www.home-assistant.io/) with an animated sky, current conditions, a 7-day forecast and a live rain radar. The compact card shows the temperature over a sky that matches the weather, day or night. Tap it to open the Weather, Forecast and Radar tabs, where every tile, hour and day opens its own detail view with graphs you can drag a crosshair along. You can choose the Classic dark look or a liquid-glass look in light or dark. Optional AI features add an outlook, weather and home heads-ups, the best time for things, questions about the forecast, spoken briefings and weekly summaries. Everything can be set up without writing any YAML.

> ✨ **AI features are optional.** Nothing AI-powered runs until you turn on AI features and choose a conversation agent in the editor (see [AI Features Setup](#-ai-features-setup-optional) below). Without an agent, the card works fully as a weather, forecast and radar card.

---

## ✨ Features

### Compact card
- **Animated sky** that follows the current condition and switches to night after sunset: sun, cloud, rain, snow, fog, thunder and a starry sky.
- **Temperature, condition, today's high and low**, a humidity pill and, optionally, wind.
- **Sky extras**: now and then something unexpected passes through the sky (see below).
- Tap to open the full card. Long-press for the weather entity's more-info.

### Sky extras
Every so often, roughly once every half a minute or so, a surprise appears in the compact card's sky:

| Extra | What happens |
|---|---|
| 🛸 **UFO** | An alien saucer drifts across, with a little alien waving from the window |
| 🚀 **USS Enterprise** | The NCC-1701 warps across the sky |
| 🟩 **Borg Cube** | The cube arrives and locks its tractor beam on to the Sun or Moon — resistance is futile |
| 🌀 **Stargate** | The gate forms in the sky and opens with the SG-1 "kawoosh" into a shimmering wormhole |
| 🐦 **Angry Birds** | Red, Yellow, Blue, Black and Bomb birds fly across in an arc |

They sit alongside the everyday sky, which has birds, planes, drifting clouds, rain, snow, fog, lightning and stars. All five extras are on by default, and each has its own switch in the editor's **Weather** section.

### Weather tab
- **Hero**: the condition icon, the temperature, and pills for "Feels like", the high and low, and a "3° warmer than yesterday" comparison from your Home Assistant history.
- **Condition tiles**: humidity, wind, pressure, UV index, visibility, dew point, cloud cover and precipitation (whatever your weather service reports).
- **Hourly strip** for the next 12 hours, with rain chance.

### Forecast tab
- **Day chips** for the next 7 days.
- For the chosen day, a **temperature graph**, **rain-chance bars** and a list of its hours.

### Radar tab
- **Live rain radar** animation over a map centred on your postcode, with a rainfall legend and the frame time.
- **Map style**: Standard, Dark or Light. You can also set the radar opacity, animation speed and zoom.

### Details and graphs
Everything on the Weather and Forecast tabs is tappable:
- **Each condition tile and the temperature** open a view with tiles for now, the last 24 hours, the change since yesterday and the next 24 hours. It also shows one graph covering the last 24 hours from history and the next 24 hours of forecast, plus a short plain-English note about what the numbers mean.
- **Each hour** opens its full details, with that day's temperature and rain graphs and the hour highlighted.
- **The outlook box** opens the outlook, each heads-up, and graphs for the next 24 hours.
- **Crosshair**: press and drag along any graph to read the value and time in a glass pill.

### Appearance
- **Style**:
  - **Classic** is the dark weather look.
  - **Glass** is a frosted, see-through surface with blur, soft highlights and rounded corners.
- **Theme** for the Glass card: Auto (follows Home Assistant), Light or Dark.
- **Glass** slider, from clear to frosted.
- The sky animation and radar map look the same in both styles.

### AI features (optional)
You need a Home Assistant conversation agent for these:
- **Today's outlook**: a one-line outlook on the compact card, for example "Dry until 3pm, then heavy showers — take a coat", and a longer version on the Weather tab.
- **Weather heads-up**: a short note when frost, heat, strong gusts, very high UV, thunderstorms, snow or heavy rain are on the way. The card spots the conditions itself, and the AI only writes the wording. It shows in yellow on the compact card.
- **Smart heads-ups**: the heads-up also checks your home. For example, "Rain in about 40 minutes and the Bedroom Window is open", "Strong gusts on the way and the Patio Awning is out", or "Frost tonight and the Living Room heating is switched off". It only reads your window, door, awning and heating entities and never changes them. It updates straight away when something opens or closes.
- **Best time for…**: tap a suggestion such as "Dry the washing", "Go for a walk" or "Cut the grass", or type your own. The card finds the best window in the next 48 hours.
- **Ask**: ask a question about the forecast, tap a suggestion, or tap **Ask about this** on any detail view or crosshair point. Answers only use your weather service's data.
- **Announce**: a spoken weather briefing played on the speakers you tick. Speakers are grouped by area, unavailable speakers and TVs are hidden, and nothing is ticked when Announce opens. It uses Home Assistant's text-to-speech and also works with Music Assistant speakers.
- **This week**: the warmest and wettest days, the next 7 days, and a summary that compares them with the last few days of recorded weather.
- **What happened?**: the last 24 hours from history, with the high and low, each change in conditions and a short recap.

Each feature has its own toggle in the editor. Ask, Best time and Announce have buttons on the Weather tab, and everything else is in the **⋯** menu. Nothing on the card itself mentions AI, and problems show as plain messages such as "Busy right now". Weather and entity data are treated as data, never as instructions, and everything is escaped before it's shown.

---

## Configuration

Add the card from the card picker, then choose your weather entity, postcode and style in the built-in visual editor. You don't need to write any YAML. The README lists every YAML option.

---

## 🤖 AI Features Setup (Optional)

AI features stay off until you turn them on and choose a conversation agent. **Google Gemini** is the recommended and best-tested agent:

### Step 1 — Enable the Generative Language API

1. Go to [console.cloud.google.com](https://console.cloud.google.com) and sign in
2. Create a new project (or select an existing one)
3. Go to **APIs & Services → Library**
4. Search for **Generative Language API** and click **Enable**

> ⚠️ Don't skip this step. An API key won't work until the Generative Language API is enabled; it will return errors straight away.

### Step 2 — Create an API Key

1. In Google Cloud Console go to **APIs & Services → Credentials**
2. Click **+ Create Credentials → API key** and copy the key

### Step 3 — Add Google Generative AI to Home Assistant

1. In Home Assistant go to **Settings → Devices & Services → + Add Integration**
2. Search for **Google Generative AI** and select it
3. Paste your API key and click Submit
4. The recommended model settings work fine. If you choose a model yourself, pick a **current Flash model**, because Google retires older models regularly (`gemini-2.0-flash` was shut down in June 2026).

### Step 4 — Configure the Card

In the card's visual editor, open **AI Features**, turn on **Enable AI features**, and choose your Google AI agent under **Conversation agent**.

### Rate limits

Free-tier limits vary by model and change over time, so check Google AI Studio for your current quota. The card caches every answer: the outlook and heads-up refresh every 30 minutes, and everything else only runs when you open it. You're unlikely to reach the limit in normal use. If you do see a quota message, it resets the next day.

If the agent can't answer, the card shows the reason in plain English and a **Try again** button. It retries once automatically first. If the outlook or heads-up can't be made, they're simply left out, and a heads-up still shows in plain words.

---

## 🌐 Where the Data Comes From

- **Conditions and forecast** come from your Home Assistant weather entity, for example Met Office, Met.no, OpenWeatherMap or Pirate Weather. What the tiles, hours and graphs can show depends on what your service reports.
- **The last 24 hours**, **compared with yesterday**, **This week** and **What happened?** use Home Assistant's recorded history of the weather entity. The recorder keeps it by default. If yours doesn't, those parts say so.
- **The radar** uses [RainViewer](https://www.rainviewer.com)'s free radar tiles, on [OpenStreetMap](https://www.openstreetmap.org/copyright) or [CARTO](https://carto.com/attributions) maps. Your postcode is looked up once with OpenStreetMap's Nominatim to centre the map. The map library (Leaflet) loads from unpkg.com the first time you open the Radar tab.
- **Best time for…** needs an hourly forecast. Most weather services provide one, and the card tells you if yours doesn't.
- **Smart heads-ups** look at `binary_sensor` entities with the `window`, `garage_door` or `opening` device class, `cover` entities with the `window`, `garage`, `awning` or `shade` device class, and `climate` entities.
