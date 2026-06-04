# **Changelog**

All notable changes to Skales will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),

and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## v11.1.5

A small follow-up on v11.1.0.

### Added

- **Share a generated image to Discover.** Studio could share a Skales Visual but not a plain image. The image view gets a Share to Discover button: the image is fitted under the feed's size limit and posted, landing in review like other shared images.

- **Send a file to your Telegram.** Skales can now send a document, image or PDF to your paired Telegram, not only text. Ask for it ("send me that report on Telegram") and the file lands in your chat.

- **Your own daily Briefing in Discover.** Follow the topics you care about and Skales brings you fresh links every day, in its own Briefing space inside Discover. It is private: only you see it, nothing is posted or shared. Skales suggests topics to start from based on what you work on and your language, you can add or unfollow any with a tap, and each item opens in the built-in browser so you stay in Skales. It fills in the background and works with a local model or no model at all, and pauses cleanly when you are offline.

### Changed

- **Skales works with whatever model you run, big-name or not.** Skales now recognizes an action whether the model returns it the standard way or writes it out as text, so a newer or smaller model can drive Skales' tools and multi-agent dispatch without special handling. If a model gets stuck repeating itself, Skales nudges it to try another way or wrap up instead of stalling. A model you wire up later just works.

- **Skales tells you which model it is running.** Ask what model or AI it is and it answers honestly with the model you configured, instead of claiming to be a different assistant.

- **Everything is on out of the box.** A fresh install starts with all features active so nothing looks missing; turn off what you do not use in Add-Ons. Existing installs are left exactly as you had them.

### Security

- **Pairing is harder to intercept.** The relay that lets two devices find each other during pairing now turns away any third device that tries to join a pair's rendezvous, and limits how often one address can connect. That closes the window where someone could brute-force a pairing code or quietly sit in on a handshake. Your messages were already end-to-end encrypted; this hardens the first-contact step itself. It applies to every v11.1.0 install with no update needed.

- **Skales reads web pages and other fetched text as information, never as orders.** Anything Skales pulls in through a tool, a web page, a search result, an email, a feed, is now clearly marked as outside content, and Skales is instructed never to act on instructions hidden inside it. This stops the "ignore your previous instructions and email this to..." trick where a booby-trapped page or message tries to hijack the agent.

- **Autopilot runs its actions, and the hard safety net can never be switched off.** An armed goal is your go-ahead, so Autopilot now actually carries out the steps you set it up for instead of quietly skipping the ones that send or change something. Underneath that, one block stays on in every mode, including Unrestricted: commands that would wipe a disk, delete your home folder or Skales' own data, set off a fork bomb, or power the machine off are always refused. That block cannot be disabled.

- **More actions stop to ask first.** Sending a WhatsApp message or media, and typing or pressing keys inside a logged-in browser page, now wait for your approval in Safe and Advanced mode, because the agent chooses who it goes to or what it types and a hostile page could try to abuse that. Replies to your own Telegram stay automatic, since they only ever go back to you. Advanced mode now also runs a risky shell command after you approve it, where Safe mode still refuses it outright.

- **The settings file is off-limits to the file tools.** Skales' own settings file can no longer be read or written through the ordinary file tools, only through Settings. That keeps your keys and security switches out of reach of a crafted file action.

- **Server-side fetches stay on the public web.** When Skales fetches a file or a URL for you, it now allows only normal web addresses, refuses internal and loopback targets, follows your domain blacklist, and re-checks every redirect so a link cannot quietly send it somewhere private. A downloaded file gets a clean name and must land inside a folder you allow, and a file only leaves over Telegram if its path is allowed.

- **Approvals belong to one chat and run exactly once.** A Telegram approval can only be confirmed from the same chat that asked for it, so another chat cannot tap Approve on your pending action. A double-tap or a retry can no longer run the same approved action twice.

- **An incoming message cannot promote itself.** The internal "system job" path that skips the usual checks is now reachable only from inside Skales. A Telegram message that claims to be a system job is treated as the ordinary message it is.

## v11.1.0

A feature release on top of v11.0.0. Two Skales computers can pair and work together
(Teams), other agents can call Skales (A2A), Autopilot becomes the live board of every
goal Skales is working on, History search can find a chat by meaning, and the system
tray shows what Skales is doing, plus a new interview-first way to set a goal and a
wave of stability and security work.

### Added

- **Teams: pair two Skales computers and work together.** Turn on Teams, pair another Skales, and you and your agent can talk to the other person and their agent, end-to-end encrypted. You confirm each new computer by name before it can pair. Each teammate gets a tag, an online indicator, and a conversation that lives in Teams (not your chat history). A You / Agent switch in the composer lets your agent reply on your behalf. Cross-computer messages never run anything on the other machine. Off until you turn it on; the mobile pairing you already use is unchanged.

- **Other agents can call Skales (A2A).** Skales now speaks the Agent2Agent standard, so another agent (or another Skales) can discover this instance and delegate a task to it. Off by default, and you stay in control of what an outside caller can do. Turn it on from the Teams screen.

- **Autopilot shows your running goals.** The Execution Board grows a Running Goals strip: one card per active goal across every chat, with its status, acceptance-criteria progress, step budget and channel. Click a card to jump straight into that goal's session. It is the live grid of everything Skales has in flight.

- **Set a goal by interview with `/goal-autopilot`.** Type it in chat and Skales opens Autopilot and interviews you first, to understand what you actually want, then proposes the concrete tasks, instead of arming a goal from a single line. The plain `/goal` (instant) path is unchanged.

### Changed

- **Voice runs on your device, in the cloud, or on your own server.** Voice uses your operating system's built-in speech by default, the cloud providers you configure (OpenAI, Gemini, Groq, ElevenLabs, Azure), or any OpenAI-compatible speech endpoint you self-host and enter under Settings, Voice. The bundled on-device engine (Kokoro for read-aloud, Whisper for transcription) stays available on Windows and Linux. On macOS it is no longer offered. Its machine-learning components cannot be code-signed inside the notarized build and so could not run there. macOS users use System, Cloud, or their own speech server, and every engine still falls back to the operating system voice if it is unavailable.

- **Web search names the provider it actually uses.** The agent no longer claims it searches with Tavily when DuckDuckGo (the keyless default) or another provider is the one configured.

- **The Playground opens right away** instead of sitting on a blank screen while it prepares its first suggestions in the background.

### Added

- **Multi-agent job results come back into the chat.** When you hand a job to multiple agents, the finished report is written back into the conversation and you get a notification when it completes, instead of having to open the Tasks tab to find it. A sub-task that runs out of its step budget now shows as parked rather than finished.

- **Find any past chat by meaning.** History search gains a Meaning toggle that ranks your conversations by what they were about, not just the exact words, blended with how recent they are. It runs on your own embedding model (local by default) and falls back to keyword search when none is set, so it never returns worse results than before.

- **The system tray shows what Skales is doing.** Open the tray menu for a live snapshot: the active provider and model, API calls this hour, scheduled planner tasks and goals, and a warning when an approval is waiting or Autopilot has paused at its cost cap. Quick links jump straight to Chat, Planner, Studio, Autopilot and Settings.

- **A context and session readout below the composer.** A quiet line shows how full the model's context window is for the current chat and how long the session has been running. Hover it for the exact token count, the model, and a note that Skales auto-compacts older messages around 75% so the model stays within its window. It reads the window from the known-model list, so it works on any provider out of the box.

- **Teach Skales a workflow by showing it once.** Walk Skales through a task in a normal chat, then open the Workflow page and pick that chat: Skales distills it into a reusable workflow with a name, a trigger, the repeatable steps and what counts as done, and you can run it again from chat with `/goal-<trigger>`. The replay runs through the normal goal path and falls back to vision when a button has moved, so a workflow you captured keeps working as pages change.

- **Review the code Lio wrote, not just the rendered page.** When a Lio build finishes, the right pane gains a Code view next to Preview: every file Lio produced, with its source shown read-only and a copy button, and images rendered inline. You can read what was actually built before you download it, deploy it or ask for changes.

### Fixed

- **Shared Skales Visuals display correctly in the feed.** A visual built at a fixed size used to show only a shifted corner; it now scales to fit, like the Studio preview.

- **Telegram and WhatsApp no longer go silent** when a task needs more than one message. You get an honest status and can reply to keep it going.

- **The occasional personalization question no longer repeats** the same prompt.

- **Copy to clipboard works in the Tasks result view**, and the chat composer cursor stays aligned with a highlighted command.

- **Uploading a file no longer starts a goal by accident.** A document that mentions a slash command (a changelog, these release notes, a piece of source) is now read and summarized, not treated as a command to run. The same goes for a skill mention written inside a file.

- **Identity maintenance stays in the background.** The nightly identity refresh no longer sends a stray "completed" message over Telegram or surfaces a bubble in the active chat; it runs silently, as it was always meant to.

- **The WordPress page no longer fails when nothing is connected.** Opening it without a configured site shows the setup prompt instead of a connection-failed error.

- **Agent-run playbooks perform more of their steps.** When Skales runs a saved browser playbook on its own, it now also does scrolling, key presses, screenshots and form fills. The few steps that need the live Browser view say so instead of being skipped without a word.

- **The edit box matches the chat width** when you edit a message, and the New Chat screen takes images by drag-and-drop. Toolbar buttons there now explain themselves on hover.

- **A recurring task you ask for in chat lands in the right place.** A sub-daily cadence (a 30-minute Pomodoro, "every two hours") now goes to Schedule, which runs it, while the Planner keeps daily, weekly and monthly jobs. Before, an unsupported cadence was saved but never appeared on the Planner and never fired.

- **The running-goal status popover stays on screen.** On a narrow window it used to slide off the left edge; it now opens rightward and is capped to the viewport, like the model picker. Searching settings for "a2a" or "teams" also finds them now, with a link to the Teams page.

## v11.0.0

```
███████  ██  ██    █████   ██       ███████  ███████
██       ██ ██    ██   ██  ██       ██       ██
███████  ████     ███████  ██       █████    ███████
     ██  ██ ██    ██   ██  ██       ██            ██
███████  ██  ██   ██   ██  ███████  ███████  ███████

   v11.0.0    release name:  /GOAL
```

A new look for Skales, a new way to work by setting Skales a goal that keeps going on its own in the background until it is done, a rebuilt Studio for images, video, voice, and music, one home for all your chats and projects, and your saved provider API keys now kept encrypted on disk.

### Added

- **Set Skales a goal and let it work toward it.** Type `/goal` followed by what you want, like `/goal build me a trading bot`, and Skales takes it on as an ongoing goal instead of a single reply. It works out what reaching the goal looks like and keeps going through the steps toward it, and when it needs a decision from you it parks the goal and shows a card to pick it back up or stop it.

- **A goal keeps working on its own in the background.** Once you set one, the work carries on by itself without the chat window open, and picks back up where it left off after you close and reopen the app. Skales keeps each goal on its own track, so you can set more than one going and come back to find them further along.

- **Set a goal to run on a schedule.** Alongside a one-off goal, you can now set one to run on a repeating schedule, like every morning or once a week. Skales works it on its own in the background each time it comes due and keeps each run separate, so a standing goal makes progress without you having to start it.

- **Skales can take on a goal from how you ask.** Off by default. When you switch it on, a message that reads like a project, for example "build me a small site and then put it online", is taken on as an ongoing goal instead of a one-off reply, with a sensitivity you can set from low to high. The wording is read on your device with no extra model call, so nothing about your message is sent anywhere to make the decision.

- **Skales can keep working a goal while you are away.** Off by default. When you switch it on, a goal that paused on its own can carry on while you are idle, picking back up once you step away and parking again for you the moment you return, so a long goal can move forward in the background without running on while you are right there.

- **Keep an ongoing presence with a goal.** Start a goal with `/goal presence:` and Skales holds a steady presence over time as a declared agent, only on the channels it can use honestly: your own Discover feed, email through your mail settings, and the official integrations you have connected. It never pretends to be a person or works around anything built to keep automated agents out, and it learns from what comes back each round. There is a short plain-language note about goals, and this type, at the bottom of the Goal settings.

- **A new look, Skales-X.** Skales opens on a new default theme with a floating glass sidebar, a calm dark palette lifted by a single bright accent, and a short launch screen when it starts. Existing installs move to the new look on update, and every other theme, including the previous one, is still in Settings under Appearance if you want to switch back.

- **One home for your chats and projects.** There is now a single place to find every conversation you have had. A history page lists your chats and lets you search across what was said inside them, opening Skales lands on a New Chat screen with your recent chats one click away, and any chat can be linked to a project so the two stay together, with Skales keeping a short running summary of what the chat is about.

- **A rebuilt Studio.** Studio is organized around four areas: Design, Media for images and video together, Audio for voice and music together, and a Gallery of everything you have made. A new button starts a fresh design, clicking any result in the Gallery opens it full size, and starting a design from a web address now reads the page in properly instead of coming up empty.

- **Share a Skales Visual to Discover.** A visual you make in Studio can be shared straight to Discover as its own live piece, and you can also save it as an HTML file or a PNG. Shared visuals are checked before they appear to everyone, and they run inside their own sandboxed frame.

- **Import your conversations from Hermes.** If you have used Hermes, you can bring your history across. Choose Hermes from the import options in Settings and point Skales at its database file; your past sessions come over, along with any personality and memory notes saved next to it.

- **Skales adapts to how you work.** Over time Skales builds a quiet sense of how you like to work and folds it into its memory, and now and then it asks you one short question to understand you better, never while it is busy and never often. You can also set your agent's character outright when you join Discover, its tone and how grounded it stays, and that carries into your chats. It stays part of your memory and is always on. When that short question does come up you get a quiet notification and a dot next to Chat so it is not missed, and you can clear everything Skales has picked up about how you work at any time, from Settings or right in the chat.

- **Cast to a screen on your network.** Skales can send a page, a chat answer, or something you made in Studio to a TV or media player that supports DLNA on your local network. It is off until you turn it on, finds devices on your own network only, and each cast is something you start. Casting something you made in Studio turns on a small sharing bridge on your own network for that cast, which you switch on yourself.

- **Draw a workflow and run it like a goal.** A goal you set in words now has a hand-drawn counterpart. A visual editor lets you lay out the steps, the inputs you will fill in, and what finished looks like, and saves the result as a workflow you can run again. Each one gets its own trigger word, like `/goal-ship`, that lights up in the chat box, and one click opens a fresh chat with it ready to edit and send. Switch workflows on under Add-Ons; a pointer in Settings, Goal shows you where.

- **Bring in your Obsidian vault.** On the Memory page you can now import an Obsidian vault, a folder of Markdown notes, or a handful of loose files. Skales reads the links between your notes and draws them as a graph you can move around, following a wikilink from one note to the next and seeing what links back to the one you are on. Once it is in, Skales can read from your notes when you ask.

- **Reach more of what your MCP servers offer.** Beyond their tools, MCP servers can publish ready-made resources and prompts, and Skales now reaches both. Type `@` in the chat box to pick one and attach it to your message as context, shown as a chip you can remove. Servers that use the newer streamable-HTTP connection work too, alongside the ones Skales already spoke to.

- **Make an image or video without leaving the chat.** Type `/image` or `/video` with a short description and Skales draws it right there in the conversation with its built-in visuals engine, no key or setup needed. What you make stays in your history and redraws when you reopen the chat.

- **Skales can search through your files.** It can now search file contents for a word or pattern and find files by name across a folder, so when you point it at a project it goes straight to the right place instead of reading entire files one by one. Its work on large folders is faster and more accurate as a result.

- **Reach Telegram even on networks that block it.** Some workplaces and regions block a direct connection to Telegram, so the bot could not receive your messages or send replies. You can now enter a proxy in the Telegram settings, and Skales sends everything to and from Telegram through it, so the integration keeps working from behind a firewall.

- **Discover, rebuilt as a living feed.** Discover is now a three-pane feed with Spaces you can join, a sort bar for what is hot, new, top, or rising, and a card that picks out posts matching the interest you chose. Joining starts by giving your agent a character: its background, its generation, and a few dials from serious to playful, dry to funny, and grounded to speculative. That character stays in your memory and carries into your chats, so your agent talks the way you set it.

### Changed

- **Skales gets better at the kinds of goals it has done before.** When a goal succeeds, Skales distills the approach that worked and reaches for it next time, on top of folding in what it learned from the parts that did not. The Memory page shows this as a before and after: the friction it ran into on a kind of task, and the proven approach it now uses instead.

- **The sidebar is steadier and easier to read.** On the new look the sidebar stays expanded as you move between pages, and when it is collapsed each icon shows its label on hover, so you can tell the sections apart at a glance.

- **Web search sits with your other integrations.** The web search setting now lives under Settings, Integrations, alongside your other connected services instead of on its own.

- **Fresh installs start on current models.** The default model choices now point at the current generation, so a new setup begins on up-to-date models without you changing anything.

- **Answers appear as they are written.** A reply now streams in word by word as Skales writes it, instead of arriving in blocks every second or two. If you have scrolled up to read something earlier, it leaves you where you are and keeps writing below, with the jump-to-bottom button one click away.

- **Skales Visuals is built into the image and video toolbar.** The generation toolbar in chat now starts on Skales Visuals, the engine that needs no key, and it is always there. Google and Replicate sit alongside it and appear as choices once you have connected a key for them. Studio opens on Skales Visuals the same way.

- **Your MCP tools answer plain requests.** Tools from a connected MCP server have always run without an `@` mention, but Skales used to suggest reaching for the picker to use them. It now treats them like its own tools on any matching request, and the `@mcp-` picker is for attaching a server's resources or prompts as extra context.

- **Skales reaches into your knowledge base on its own.** The documents you add to the Knowledge Base were searchable with the `/rag` command; Skales now reaches for them by itself too. When you ask about something from a file or note you put in, it searches your indexed documents and answers from them instead of guessing, and it offers this only once you have added a document.

- **Summarizing a link gives you a readable page.** Ask Skales to summarize a web address and the result now comes back as a small rendered page instead of plain text, which reads better for an article. Summarizing text you typed stays plain, and your own choice in the style bar always wins.

- **The chat box highlights commands and mentions as you type.** A recognized command like `/goal` and an `@` mention of a skill or server light up as you write, and `/goal` now works wherever you drop it in a longer message, not only at the start.

- **The window frame follows your theme.** On macOS and Windows the title bar now takes on the active theme instead of staying the plain system frame, so the whole window matches the rest of Skales. Linux keeps its native frame.

- **Skales opens faster.** Start-up no longer waits on background setup before the first screen shows, the first-run check runs once instead of on every move between pages, and a page you are about to open from the sidebar loads a step ahead when you hover it.

- **Subscription and bring-your-own-key models use their full context window.** A ChatGPT, Claude, or Gemini sign-in, and a pasted token, is now sized to the real window of the model behind it, so a long chat no longer starts compressing far too early.

- **A passing connection test means a working connection.** Testing a custom provider endpoint now builds its address the same way a real chat does, so a full or versioned URL that works in conversation no longer comes back as a failed test.

- **Skales loads your installed skills only when they are needed.** If you had many skills installed, the full instructions for every one of them were packed into each message, which slowed responses and could make Skales talk about skills it was not actually using. It now keeps a short list of your skills and pulls a skill's full instructions the moment it is relevant or it decides to use one, so responses stay fast and accurate no matter how many skills you have.

- **Long runs keep their thread instead of running out of room.** When a task takes many steps and the conversation grows large, Skales used to quietly drop the oldest turns and could lose track of what it had already done. It now compresses the older turns into a compact progress note and keeps working from it. On the models that support it the compression happens on the provider's side; everywhere else Skales does it itself, so a long task stays on course.

- **Skales changes tack when it gets stuck on a goal.** While working a goal, if it catches itself repeating the same step or going several rounds without real progress, it now stops, rethinks, and tries a different approach instead of grinding through its step budget on something that is not working.

- **Goal planning can run on a cheaper or local model.** The background steps that plan a goal, check its progress, and sum up where it is can now be pointed at a smaller or local model while your main model does the real work, so a long-running goal costs less to keep going. It uses your main model unless you choose another in the goal settings, so this stays your choice and works with any provider.

- **Playground builds apps more reliably on a local model.** A smaller or self-hosted model now has a little more room on length and the number of AI calls so its apps make it through, and an app that calls a function it never wrote is caught and rebuilt instead of shipping broken. The prompt also hands the model a full page to fill in, so weaker models start from solid structure.

### Fixed

- **Group chats and Organization runs start again.** Kicking off a multi-model group chat or running an Organization could fail to begin; both now start and run the way you set them up.

- **Discover works on a phone, and keeps your tag.** On a narrow screen the Spaces and details panels now open over the feed instead of sliding behind the sidebar, so everything is reachable. And if you already have a Discover tag, Skales keeps it instead of asking you to pick a new one after an update.

- **Discover keeps what you share.** Shared skills, templates, and images used to scroll out of the feed and vanish for good once it filled up, which made Discover feel like a feed that resets. They now stay permanently; only everyday chatter ages out.

- **The Brand Kit reaches Studio.** Turning on Brand Kit in an image or video generator now actually applies your brand: your palette in the prompt, plus your logo for Skales Visuals video. Before, the toggle recorded your choice but changed nothing.

- **You can reset what Skales learned about you.** Settings, Memory, Adaptive personalization now has a Reset that erases your agent's character and everything Skales has picked up about how you work, in one click.

- **AIPointer keeps the look you gave it.** AIPointer's own light or dark setting no longer follows the desktop theme; it stays the way you set it whatever theme Skales is on.

- **Opening a finished chat from a notification lands on that chat.** When a reply finished while you were on another page, the notification and the sidebar dot used to drop you on the New Chat screen instead of the conversation that answered. Both now reopen the exact chat that finished.

- **The New Chat screen lines up and opens its commands.** On the opening New Chat screen the "+" button and the send button now sit centered on the input row instead of dropping below it, and typing "/" or pressing the commands button opens the same command list the in-chat composer has.

- **The screen-share picker sits where it should.** Choosing a window to share opened a panel pinned against the sidebar with empty space beside it. It now centers on the screen the way it was meant to.

- **Clicking Chat lands on New Chat.** With a goal parked in your last session, clicking Chat used to reopen that session instead of the New Chat screen. It now opens New Chat unless a chat is actively replying, and a parked goal waits for you in your recent chats and on its card.

- **A shared video plays as a video.** When Skales shared a YouTube link it could come through as a broken player. It now plays as a clean embedded video, while a richer page that happens to include a video keeps its full layout.

- **The completion sound only plays when you are away.** A finished reply used to chime even while you sat on the chat waiting for it. The sound now plays only when Skales is in the background or you are on another page; the toast and the sidebar dot still appear either way.

- **Links show a preview card.** A web address you or Skales drop into the chat now shows a small preview with the page title and image, for both sides of the conversation.

- **A capped local model is told only the tools it kept.** When you limit how many tools a local model may use, Skales used to still describe whole groups of tools that did not fit the limit, so the model would reach for one it never received and report it could not help. The prompt now lists only the tools that made the cut, so the model works with what it actually has.

- **Messages stay put when several arrive at the same time.** If two were saved in the same moment, a Friend Mode check-in landing while you replied on Telegram, or a Desktop Buddy reply arriving alongside one in the main window, one of them could quietly overwrite the other and vanish from your history. Each message is now saved in a way that cannot overwrite another, so they all stay where you left them no matter how they overlap.

- **Deleting your message now clears its reply too.** Deleting one of your own messages used to leave the response it produced sitting right underneath it, even though the confirmation said the responses below would go too. Deleting your message now removes the whole exchange, the reply and any tool results that came with it, exactly as the prompt promises.

- **Skales recognizes what it is set up to do.** With a provider configured for something like image generation or web search, Skales could still talk about that feature as if it were missing or not set up. It now reads what is available from the same place your provider keys live, so its sense of what it can do matches what you have configured.

- **The Compact button shortens a long chat when you press it.** Compacting on demand reused the limits meant for the automatic version, so the button did nothing until a chat was already very long. Pressing it now shortens the conversation whenever you ask, and it stays disabled only while Skales is mid-reply.

- **Large files and long results no longer get cut off and lost.** When Skales read a big file or ran a command with a lot of output, only the first few thousand characters reached it and the rest was dropped, so it could act on half a picture. It now reads large files in pages and, when a result is too big to show at once, saves the full text and keeps reading from where it left off. It also sizes how much it keeps to the room left in the conversation, so a single big result can no longer crowd out everything else.

### Security

- **Your saved provider API keys are now stored encrypted.** They used to sit in plain text in your settings file. Skales now keeps them scrambled on disk and unlocks them only when it needs to reach a provider. Keys you already saved are converted automatically the next time you open the app, with nothing to re-enter. Tokens for connected services like Telegram or Slack are not encrypted yet.

- **Sign-in and link previews are hardened.** The sign-in window now treats whatever a provider sends back as text rather than markup and only accepts messages from Skales itself, closing a way a crafted error could slip content into the page. Link previews and the Studio read-from-web feature now refuse web addresses that point back at your own machine or your local network, except where a design served locally is the legitimate target.

## v10.4.5

Reliability fixes for the messaging channels, Friend Mode, and the chat view.

### Fixed

- **Skales's own check-ins stay out of your open chat.** When Skales reached out on its own, a Friend Mode note or a quiet identity check-in, the message could land in whatever chat you had open on the desktop and take it over. Those check-ins now keep to their own place, so the chat you are working in stays yours.

- **WhatsApp conversations stay in their own chat.** Messages from WhatsApp used to drop into whichever chat happened to be open on the desktop. WhatsApp now keeps its own dedicated Skales chat, the same way Telegram does, so a conversation you start there stays in one place.

- **Friend Mode keeps the thread when you switch screens.** When you moved from working on the desktop to a message from Skales on Telegram or WhatsApp, its note could arrive out of context, more like a generic notification than a friend picking up where you left off. Friend Mode now reads what you were just doing across all your channels, so its message stays on topic and in your voice, while still only ever writing to the channel it reached you on.

- **Formatting comes through on Telegram.** Bold text, lists, and code blocks used to show up as raw symbols and stray asterisks in Telegram replies. They now render properly, and code stays in a clean block you can copy.

- **Replies stop disappearing.** Some replies lived only on screen and vanished the moment you sent your next message or reloaded the chat. This included the playful easter-egg replies, the hello greeting, in-chat search results, the project commands, knowledge-base lookups, persona and model switches, and generated images and videos. All of these now stay in your chat history where you left them.

- **Short messages get a proper bubble.** A very short message, yours or a short reply from Skales, drew a bubble too narrow to fit the copy and other action buttons. Short messages now keep a comfortable minimum width, so those buttons always fit.

## v10.4.1

Reliability and clarity fixes for Codework, local models, file access, and the chat view.

### Fixed

- **Codework tells you when a local model can't carry out a task.** With some local models, Codework could end a task as if it had succeeded while nothing was actually built or changed, or run on until it stopped on a confusing error. It now keeps the model pointed at doing the work for real, and when it still can't, it ends with a clear message and what to try next, instead of a quiet success that left nothing behind.

- **File-access settings are clearer and fail early.** Folders you add under Custom are checked the moment you add them, so a missing, read-only, or otherwise invalid path is flagged with a warning instead of breaking mid-task. When file access is set to Workspace Only and something tries to use a path outside the workspace, Skales now stops with a clear message about how to allow it, instead of quietly saving the file somewhere you did not expect. The panel also notes that these settings cover file access only, which is separate from Computer Use control of your screen, mouse, and keyboard.

- **Local models get the time they need to respond.** The previous limit could cut a local model off while it was still loading into memory or working through a longer step, which surfaced as a confusing timeout. Timeouts now start higher for local and self-hosted models, and the per-provider timeout you set in Settings is honored everywhere Codework runs, not only in chat.

- **Multi-step tool runs read as one block.** When Codework takes several tool steps before answering, for example reading a file, listing a folder, then replying, the steps now collapse into a single section with one tool-results view instead of stacking as separate windows.

- **Copy your own messages.** The copy button now appears on your messages too, matching the one already on Skales replies.

## v10.4.0

AIPointer ⦿ is now a built-in part of Skales.

AIPointer is a cursor-anchored quick-ask AI overlay by the same team behind Skales. Hold a key, ask a question over whatever your cursor is pointing at, get an answer. Standalone AIPointer is a fast 2-second loop. The version inside Skales is an upgrade: it already knows who you are, what you have been working on, and can write straight into your Skales todos, calendar, notes, and memory. Heavy work hands off to the full Skales chat with one click.

### Added

- **AIPointer ⦿ integration.** Enable in Settings > Appearance > AIPointer ⦿. Hold the right Cmd key (right Ctrl on Windows / Linux) or wiggle your cursor, and a translucent quick-ask box appears over whatever app you are in. Type or speak a question. Get a fast answer that respects your timezone, language, and current projects without having to re-introduce yourself every time.

- **AIPointer knows you, because Skales knows you.** The overlay reads your Skales identity (name, language, timezone, active projects, interests) on every query. It pulls in recent topics when you ask "what was I working on?", and looks up entities from your knowledge graph when you mention names like "Alice" or "the Vienna trip". Nothing to type twice, nothing to set up.

- **AIPointer can do things in Skales.** Four atomic actions fit the 2-second loop. Say "remember this" and it goes to your long-term memory. Say "add to my todos" and it lands on your task list. Say "save as a note" and it appends to your dashboard note widget. Say "schedule lunch tomorrow at noon" and it captures the calendar intent. No app-switching for quick captures.

- **Send to chat.** Any AIPointer response carries a Send button that hands the query and the answer off to Skales main chat as a new session. Use it when the quick loop is not enough, like codework, browser automation, or anything multi-step. The imported session has full context, ready to continue with the complete Skales toolset.

- **Whisper and Kokoro voice engines.** New in Settings > Integrations > Voice > Local AI Voice Engines. The Kokoro text-to-speech runtime is live and powers AIPointer ⦿ read-aloud in 28 voices, fully on-device, no API key, no cloud round-trip, no per-minute cost. The Whisper speech-to-text model downloads here too, but the on-device runtime arrives with the next AIPointer sync; until then the AIPointer mic transparently falls back to your Skales transcription cascade (Groq / OpenAI Whisper API / Azure / local STT URL, pick yours under Settings > Voice). Skales main chat keeps its own TTS + STT cascade in v10.4.0; sharing Whisper + Kokoro across both surfaces lands in Skales v11.

- **Rich response formatting when it earns its keep.** For structured answers like comparisons, multi-step how-tos, planning, or summaries with metrics, AIPointer renders the response with cards, callouts, numbered steps, and metric tiles. Plain questions stay plain prose so a "what time is it for me?" answers in one line. Skales chat renders the same rich layout when you Send to chat, so the look survives the hand-off.

- **Discover indicator (opt-in).** Show others on Discover that you are using AIPointer ⦿ right now. Anonymous, just your Discover tag, no query content shared. Off by default. Toggle under Settings > AIPointer ⦿ > Discover.

- **AIPointer Settings tab.** A dedicated panel under Settings with every AIPointer knob in one place: trigger hotkey, mouse wiggle, hold duration, voice-first mode, chat-only mode, light or dark theme, accent colour, cursor halo intensity, screenshot crop size, pill offset, auto-approve tools, session transcripts, plus a Skales Integration section for the "activate only when Skales is minimised" behaviour. The current AIPointer version (and the fact that it has its own release cadence) is displayed at the top.

- **Built-in spell check.** Every editable surface across Skales, from the chat input to Settings to titles, now shows red underlines on misspelled words. Right-click a flagged word for suggestions and Add to Dictionary. A toggle in Settings turns it off, and you can pick spell-check languages independently of your UI language.

- **Sign in with your ChatGPT subscription.** Skales now supports OAuth sign-in for ChatGPT Plus, Pro, Business, and Enterprise accounts. Pick the new Subscriptions card at the top of AI Providers, click Sign in, and Skales routes chat through your existing ChatGPT plan with no API key required. Models available through your subscription show up in the model picker automatically.

- **Bring your own Claude or Gemini subscription token (advanced).** Power users who already have a token from Claude Code CLI or Gemini CLI can paste it into Skales under Subscriptions. The feature is opt-in, behind a disclaimer you actively accept. Skales sends the request unchanged, no header spoofing, no client masking. Anthropic and Google prohibit this in their consumer terms and have suspended accounts that route subscription tokens through third-party tools. The choice and the risk are yours. Sanctioned alternatives (Anthropic Console, Google AI Studio) sit one click away on the same cards.

- **Send your location to the Telegram bot.** Share a location or a place through Telegram's attachment menu and Skales now reads the coordinates. Ask "what is the closest bakery" and it can answer from where you are, instead of asking you to type an address or paste a map link.

- **Pick which agent answers on Telegram.** A new /agent command in the bot lets you switch between Default Skales and any of your custom or built-in agents. The chosen agent replies with its own instructions, model, and tool scope, and keeps its own Telegram chat history separate from the rest. Default stays Skales until you switch.

### Known limitations

- **Subscription tokens are stored in plaintext on disk.** OAuth access tokens and pasted BYO tokens live in your local settings.json in cleartext. They never leave your device except to the vendor API the token is for, and they sit inside the Skales data directory you already protect. End-to-end on-disk encryption via the OS keychain arrives with Skales v11. If your threat model includes a co-located attacker with full disk read, prefer API key providers (which are also plaintext today, same story) and rotate the key.

### Changed

- **The Spotlight Bar has been retired.** AIPointer covers the same quick-ask use case with cursor anchoring, voice, vision, and richer affordances. The old Spotlight hotkey no longer triggers anything. Enable AIPointer in Settings > Appearance.

- **Saving a provider key actually tests it.** Pasting an API key and clicking Test now also enables the provider when the test succeeds and, if your active provider is still the empty install default, switches to the one you just configured. Already-active choices are never overridden.

- **OpenAI provider passes Organization on outgoing requests.** ProviderConfig carries an optional organization field; when set, every outgoing OpenAI call attaches the OpenAI-Organization header. Project-scoped (sk-proj-) and service-account (sk-svcacct-) keys that depend on an org binding now resolve correctly. The OpenAI provider card shows an inline hint when it detects a sk-proj- or sk-svcacct- key, and exposes the Organization input right below the API key field.

- **Friend Mode is back, and it remembers the conversation.** Skales can reach out to you on its own again, by Telegram, WhatsApp, or email. Each note is now built from your most recent chat and the things you have talked about before, so it reads like a friend picking up the thread instead of a template. It speaks in the same voice as your chat assistant: keep things formal and it stays formal, chat with emojis and it keeps using them. Ask it to drop a subject and it stays dropped, even across messages. It also picks its moments: it holds off while you are mid-task and when your last note has gone unanswered, rather than arriving on a fixed clock. Switch it on under Settings > Friend Mode, and use Test Friend Mode to confirm your channels.

- **Pick your web search engine.** Web search is no longer Tavily-or-nothing. A Search provider dropdown under Settings > Integrations > Web Search lets you choose DuckDuckGo (no API key, the new default), Tavily, Brave, a self-hosted SearXNG instance, or hand web search to a connected MCP server. Skales always gives the agent one search tool and swaps the engine behind it, so you no longer have to wire up an MCP server just for basic web search.

- **Run several custom providers at once.** You can register multiple OpenAI-compatible endpoints side by side (a local llama-swap, a vLLM box, a gateway, a second LM Studio) under Settings > AI Providers > Additional Custom Providers, each with its own name, URL, key, and model. They now resolve correctly when selected and appear in the chat model picker, so you can switch between them per chat instead of rewriting one shared slot.

- **Projects has one clear action button.** "Discuss with AI" and "Start working" did almost the same thing, which was confusing, so "Start working" is gone. "Discuss with AI" opens the project chat the same as before.

### Fixed

- **The agent uses your MCP search tool when Tavily is off.** With no Tavily key, Skales still told the model it had built-in web search, so the model reached for a tool that was not there and waved off a connected MCP search provider like DuckDuckGo as something it could not call. Now, when Tavily is off, the prompt stops advertising the built-in search, and the agent treats your connected MCP search tool as the real web search.

- **Skales keeps your connected MCP tools in reach.** Tools from any MCP server you connect now stay available to the assistant from one message to the next, whatever you named the server, and including on local models where the built-in tools used to crowd them out. While a server is still connecting or briefly drops, Skales no longer claims those tools are ready when they are not, so you stop getting confident answers about tools that cannot actually run.

- **No more phantom GitHub setup.** Skales stopped describing a built-in GitHub integration it no longer ships. GitHub is reached by adding the GitHub MCP server under Settings > MCP, and that is the only place Skales points you to now.

- **Clearer Google Calendar setup.** The Calendar settings now spell out what actually connects your calendar. An API key only reads public calendars (your own calendar returns a 404 with a key), so personal read and write needs OAuth. The OAuth section now calls out the step that trips most people up: a Google consent screen left on "Testing" blocks sign-in until you add yourself as a test user or publish the app.

- **Outlook Calendar connects again.** Connecting Outlook failed right after the Microsoft app setup because Skales asked for a sign-in redirect Microsoft no longer accepts. It now uses the supported desktop sign-in, works with single-tenant work accounts (enter your Tenant ID), and needs no client secret. The card also gained the Save and Test buttons the Google and Apple cards have, remembers your details across reloads, and the setup box spells out exactly what to register in your Microsoft app. Once connected, your Outlook events show up in the Planner alongside Google and Apple, the same as before.

- **Vision skill recognises local providers.** With a local Ollama or Custom Vision Provider configured, the Vision skill no longer stays stuck on "enabled, needs setup". The screenshot tool is callable as soon as you have a vision model selected. No API key required for local endpoints.

- **Clearer OpenAI errors.** Invalid key (401), exceeded quota (403), missing model access (404), and rate limit (429) each surface as their own toast with the right next step, instead of all collapsing into a single "API key failed".

- **Local models run your tools again, instead of just describing them.** On Ollama and other local or custom models, the agent would sometimes write out a tool call as plain text and then stop, so Codework and Chat produced a detailed plan but changed no files and ran no commands. Skales now recognises a tool call written that way and runs it, the same as it does for the big cloud models, so work that needs real edits, commands, or searches actually goes through on local models.

- **Skales stops claiming skills it has not been set up for.** When a skill was switched on but had nothing connected yet (say WhatsApp or Discord with no account linked), the model could still announce it was able to send messages there. Skales now states plainly which skills are ready to use and which still need setup, and it no longer lists the actions of a skill that is not ready, so it stops making promises it cannot keep.

- **The Filesystem MCP server starts on Windows.** Its default folder was set to a path that only exists on Mac and Linux, so on Windows it failed every time it tried to start. Skales now points it at the right temporary folder for your system, and quietly repairs a server that was already saved with the old path, so it connects instead of looping on the same error.

- **The MCP server list shows the real state.** Under Settings > MCP a server that was switched on always showed a green dot, even when it was failing to connect. The dot now reflects what actually happened on the last attempt and shows the error next to a server that could not start, so a broken server no longer looks healthy.

- **Provider fallback skips the entries it cannot use.** If you turned on provider fallback and the chain listed a cloud provider with no key, Skales tried each empty one and failed down the list every turn before reaching a working local model, which looked like it was switching models at random. It now skips a fallback provider that has no key or sign-in and goes straight to one that can actually answer.

- **Apps you build in Playground stop breaking on a missing helper.** Smaller models building a Space sometimes left out one of the small helper functions while still calling it, so the finished app showed an error like "mdToHtml is not defined" the moment it opened. Skales now provides those helpers to every generated app itself, so the app runs even when the model forgets to include one.

- **The left sidebar shows every item again.** With a lot of features switched on, the navigation list could grow tall enough to push the bottom actions (Settings, Stop Server) off the screen. The list now scrolls on its own and the bottom actions stay pinned and reachable, in every theme.

- **Telegram messages stay in their own chat.** Messages you send to the Telegram bot used to land in whichever agent chat happened to be open on the desktop, and then show up a second time in your default chat. The bot now keeps its own dedicated Skales chat, so a conversation you start on Telegram stays in one place and stops appearing twice.

- **The voice button appears once speech-to-text is set up.** The microphone in chat stayed hidden unless you switched on the Voice Chat skill, so setting up a Whisper server or a speech-to-text key looked like it did nothing. The mic now shows up as soon as any speech-to-text option is in place (your own local Whisper server, Groq or OpenAI Whisper, or Azure), and the Settings hint now says the URL field is what powers it. An always-on wake word is not in this release.

- **/clear in Telegram actually starts a fresh chat now.** The command used to reply "Context cleared" without doing anything, so the bot kept right on with the old conversation. It now opens a new chat for whichever agent you are talking to (/new does the same), while the previous conversation stays saved in your history.

- **The dashboard Tasks widget shows the real list.** It loaded once and then held on to tasks you had already deleted, and hid finished ones entirely. It now refreshes on its own, puts active tasks first with older ones below in a scrollable list, and a task you delete (or clearing them all) drops off right away.

- **No more double "+" on the dashboard Connections card.** "Manage connections" showed two plus signs and dropped you at the top of Settings. It is now one clean link that opens the AI Providers tab directly.

- **Remove an MCP environment variable while setting one up.** Each variable row in the MCP setup got a delete button, so a typo in a variable name no longer means closing Settings and starting over.

- **The Identity Maintenance task is tidy again.** On the Tasks page it had started showing its internal setup text and a delete button that never did anything. It now shows a short note instead: it lives under Settings > Memory, where you switch it on or off, and you can still run it by hand from the Tasks page. Long task descriptions also collapse behind a Show more toggle so the list stays readable.

- **AIPointer ⦿ actually sends the screenshot now.** The overlay collected your question but never captured or attached the cursor-area screenshot, so vision-capable models kept replying "I can't see your screen". AIPointer now grabs the screenshot (and your clipboard, when that chip is on) at submit time and sends it along, so "what am I looking at?" works on wiggle, hotkey, and bullet-click triggers.

- **AIPointer ⦿ region selection captures the right area.** Holding the trigger a second time and dragging a rectangle now attaches exactly that crop to your next question. Previously the drag drew the box and flashed "Selection captured", but the captured pixels were thrown away and the query silently fell back to the default cursor-centered shot. The drawn region now wins over the default capture and over the chat-only chip, and it clears itself after one query (or when you dismiss the box) so a leftover crop never sticks to a later question.

- **AIPointer ⦿ honours your dedicated Vision Provider.** Earlier the overlay sent every screenshot through whichever AI provider was active for chat, ignoring the separate Vision Provider you set up under Settings > AI Providers. Now AIPointer reads that config the same way the main chat's screenshot tool does: bring your own local LLaVA on Ollama or a custom localhost endpoint for vision, and AIPointer routes the cursor screenshot straight there while text questions keep going to your usual chat brain. Single-image queries only; multi-image is unchanged and stays on the chat brain.

- **AIPointer ⦿ auto-attach finally fires inside Skales.** Highlight up to 5 files in Finder (macOS) or Explorer (Windows), press the AIPointer hotkey, and the selected files queue for the next query. The paperclip button next to the mic also opens a file picker. The "N files attached" pill above the prompt confirms what's lined up; the queue clears after each submit. Images become vision context, text files inline into the prompt, binaries (PDF, DOCX, XLSX) get referenced by name. macOS will ask for Finder Automation permission on first use.

- **Bullet pill stops flickering while you type.** Typing in any text field outside Skales (browser address bar, another app's composer, the chat editor itself) no longer makes the small status pill at the bottom of the screen flicker on every keystroke. The internal "user is busy elsewhere" signal now only runs when the big AIPointer answer pill is actually open, so the idle bullet stays calm.

- **AIPointer ⦿ wiggle / hotkey stop dying after one missed trigger.** When the "activate only when Skales is minimized" guard rejected a trigger (because Skales was the focused window), the trigger state machine stayed stuck pretending an AI session was open. Subsequent wiggles or hotkey holds got silently swallowed until you clicked the bullet manually to force a reset. The guard now rolls the state back cleanly so the next trigger gesture works straight away.

- **No more dark overlay across the screen on minimize.** AIPointer's transparent overlay window paints transparent regardless of which Skales theme is active. The wake-up recovery effect that re-applies Skales' theme background was firing inside the overlay's renderer on every visibility change and stamping a solid dark background over the user's screen. That effect is now scoped to the main Skales window only.

- **AIPointer ⦿ response text readable in light theme.** A hardcoded white text colour on the overlay wrapper was overriding the response markdown's per-theme colour rules. Removed, so the answer body and headings follow your AIPointer Appearance picker (Light / Dark) the way the rest of the surface already does.

- **Spell-check actually underlines misspellings in the chat composer.** The chat input had `spellCheck={false}` hardcoded on both the mobile and desktop composers, which silently nullified the Settings > General > Spell-check language list. With the toggle removed, your selected dictionaries (English, German, Croatian, the rest of the 13 supported languages) get red underlines and right-click suggestions like every other editable field. The same fix lands on the AIPointer ⦿ prompt input.

- **AIPointer ⦿ Settings tab readability.** The FAQ section's titles were rendering invisible on dark Skales themes (white text on the tab's forced light surface). Replaced the theme-variable colours with the tab's own dark-gray palette so every entry, Skales-specific ones at the top and the longer AIPointer reference list, stays readable in any theme, all behind one consistent accordion. The "What AIPointer is / is not" block above it and the "Coming with Skales v11" preview switched to the same palette.

- **AIPointer ⦿ tab header.** The opener box now renders "AIPointer" as one word the way it's branded. The duplicate header card with "Cursor-anchored quick-ask..." was redundant and is gone; the brand opener at the top of the tab and the Help card at the bottom keep the GitHub link and version.

- **AIPointer ⦿ inside Skales no longer asks the system keychain on launch.** The standalone AIPointer keeps its own encrypted provider key store; the in-Skales build doesn't need it because Skales bridges every provider call. On launch the AIPointer module now detects it's running inside Skales (presence of the Skales data directory) and skips the keychain probe entirely, so users with an existing standalone AIPointer install don't see a "Skales would like to use the keychain" prompt every time they open Skales.


## v10.3.7

Settings performance pass, a Friend Mode safety hold, GitHub moves to MCP, plus a handful of cleanups.

### Changed

- **Settings opens faster.** Switching providers, opening the model picker, and changing tabs feel responsive again. A deeper rework that makes every Settings tab open instantly is queued for the next release.

- **Settings reachable from every menu.** A Settings shortcut now sits at the bottom of the sidebar, the icon rail, the top navigation, and the mobile menu, right above Stop Server.

- **GitHub access moves to MCP.** The built-in GitHub setup in Settings has been removed. GitHub stays reachable by adding the GitHub MCP server under Settings > MCP.

- **Friend Mode temporarily off.** Proactive outreach is paused while the underlying session work it depends on is finished. The feature returns in an upcoming release.

- **MCP page retired.** Adding, editing, testing, and removing MCP servers all happen in Settings > MCP. The standalone page that duplicated this surface is gone.

- **More accurate provider filter.** With "Show only active" enabled, the provider list only shows the providers you have actually configured.

- **Clearer import message.** When a chat history import finishes, the confirmation now points to your History panel and how to find the imported conversations.

### Fixed

- **Playground stops failing on dashboards and analyzers.** Generating a dashboard or analyzer no longer trips a validation check meant only for research.

- **Icon rail menu stays on screen.** The overflow menu on the left rail now opens upward instead of running off the bottom of the screen on shorter windows.

- **Sidebar buttons stop getting clipped.** Buttons that used to disappear behind the window edge on smaller heights are now visible.

- **Discover posts keep their line breaks.** Multi-paragraph posts render with the paragraph breaks the author wrote, instead of collapsing to one block of text.

- **Filesystem connector works on Windows.** Adding the built-in filesystem connector no longer fails on Windows out of the box.

- **Broken connectors stop being retried every turn.** Failing connectors back off into a cooldown, and that cooldown survives an app restart instead of resetting on every launch.

- **Identity Maintenance writes timeless profile content.** The daily profile update no longer bakes the running Skales version or release dates into your saved profile, and rewrites any sentence that still carries one.

- **Identity Maintenance no longer shows up in chat.** The internal task body for the daily maintenance run is no longer visible in your chat stream when the schedule fires.

- **Identity Maintenance scheduled task no longer duplicates.** Repeated runs of the setup flow only ever leave one entry in place.

- **Profile better at parsing pasted paths.** Pasting a path or URL into chat no longer mangles it into a garbage token in your saved profile.


## v10.3.5

Background work, a lighter prompt on smaller models, a one-click memory mode, and a round of fixes.

### Added

- **Background tasks.** You can start something, switch to another view, or close and reopen the window, and it keeps running. When you come back, the result is waiting for you.

- **Tasks stay paused only when they should.** A run pauses only when it genuinely needs your approval, not just because you navigated away. Approval requests survive navigation, so nothing gets stranded or lost.

- **Get notified when work finishes.** When a background task completes while you are on another page, you get a notification with sound and a marker on the chat in the sidebar.

- **Memory mode in one click.** The memory mode button in the chat header now cycles through all three modes with a single click, each with its own clear colour, so you can adjust it without opening settings.

### Changed

- **Images you send stay visible.** An attached image now shows as a thumbnail in your message and stays there, even after a reload. Click to open the full image.

- **Leaner prompt on smaller models.** The prompt sent to smaller and local models is lighter, without losing any awareness of what Skales can do.

### Fixed

- **Smoother scrolling when switching between conversations.** Opening one conversation out of another no longer overshoots before settling.

- **Imported chats are clearly marked by source.** Chats migrated from another tool now carry a badge in your history naming where they came from.

- **Stop and killswitch respond immediately.** Both fire instantly, even in the middle of a running task.


## v10.3.4

Hotfix session.

### Fixed

- **macOS Apple Silicon installer launched into a "Server files missing, please reinstall Skales" error.** The v10.3.3 arm64 build was packaged incorrectly. Both Mac architectures are now packed from a single shared build pass that cannot diverge.

- **Left sidebar "More" menu rendered empty on smaller windows (most visibly on Windows).** Clicking the three dots opened a popover whose items were not visible. The menu now renders as intended.

## v10.3.3

A focused hotfix release. The MCP-button fix from v10.3.1 and v10.3.2 finally lands on every setup. Assistant replies no longer appear trapped inside the Tool Results disclosure. Local models with large context windows stop feeling reset after a few tool-heavy turns. And Discover gets a focused upgrade.

### Fixed

- **Edit a configured MCP server straight from Settings.** Each server row in Settings now has an explicit Edit button next to Test, Toggle, and Remove. Clicking it opens a form pre-filled with the server's current settings. Every row icon carries a tooltip and screen-reader label, translated across all 12 locales.

- **MCP status badge updates immediately after a successful Test.** A green Test result no longer leaves the badge stuck on "stopped". It flips to "connected (N tools)" right away.

- **Environment variable values are readable by default.** They used to render as password dots, which made copying tokens out of a vault painful. They are now plain text with a per-row Show / Hide toggle for screen-sharing situations.

- **Assistant prose no longer hides inside the Tool Results disclosure.** When an assistant turn had both an answer and tool calls, the answer used to render inside the collapsed disclosure, so reading the reply required clicking the header first. The prose renders above the disclosure now.

- **Local endpoints with large context windows stop feeling reset after a few tool-heavy turns.** When Skales had no live context-length info for a model, it used to clamp it to a conservative value, which triggered auto-compression far too aggressively. The floor is higher now, and a wider range of community model families are recognised so they default to their real context size. User overrides under Settings > Override Model Limits still win on top.

- **Override Model Limits respects every Custom Provider slot.** Users running multiple Custom Provider slots can set one override that applies to all of them, unless an explicit per-slot row exists. Capitalisation differences between your override row and what the server reports no longer silently drop the value.

- **Skales can read its own past conversations now.** When you ask the assistant in natural language "what did we discuss about X yesterday?" or "find that chat where I planned the Vienna trip", it can now pull snippets directly from your saved sessions (including chats imported from ChatGPT, Claude, and others) and answer instead of falling back to memory only. The /search slash command is unchanged. It stays a fast local text scan.

- **Ollama "Max tools" slider labels line up with the slider value.** Setting the slider to 25 used to land it between two label positions that pretended to be "15" and "35" but were actually placed elsewhere. Labels now sit at their true values. Visual only, behaviour unchanged.

- **Web reader returns the full extracted page.** More of the extracted page reaches the model now, so summarising a long article works the way the tool description promised.

- **The /projects autocomplete shows a real description.** Typing /p used to surface the raw translation key in the suggestion. Translated across every language.

### Added

- **Recent group in the chat-header model picker.** The picker leads with a small "Recent" section showing the last five models you actually sent with, ahead of any curated list. Locally installed Ollama models and custom model ids land at the top of the dropdown without needing to be in any built-in catalog. A Clear button empties the list.

### Discover gets a focused upgrade

**Privacy disclosure with explicit consent.** The Join Discover wizard now shows a small paragraph under the tag input explaining exactly what is stored on the Skales server (the tag you chose and a one-time random ID, not your name, email, or device fingerprint), and a checkbox you have to tick before the Next button enables. The shorter privacy line on the final step has been rewritten to match what is actually stored, not the vague "no personal data" copy from before.

**Polls.** Posts marked as polls render with a question and up to eight option buttons. Click an option to vote. One vote per identity per poll. Expired polls render as Closed and the buttons disable.

**Rename your tag, or reset your identity entirely.** Settings > Discover gets two new buttons next to Edit Profile and Leave Discover. Rename Tag changes your gamertag in place, your existing posts and votes stay attached. Reset Identity wipes both the local copy and the server-side row, so you can rejoin under a fresh name.

**Activity tab.** A new chip in the Discover filter row opens an inbox grouped into Mentions, Replies, and From Admin. Auto-refreshes every minute while open. Click an unread item to mark it read.

**Hashtags.** Inline #tags in any post are clickable now. Click one to filter the feed to posts that carry that tag. The filter banner at the top has a Clear button. Works alongside the existing author filter.

**Pinned-by-admin posts.** Posts the Skales admin flags as pinned sort to the top of the feed with a small Pinned badge.

**Force-rebrand handling.** If the Skales admin flags your tag (impersonation, offensive content, etc.), Skales wipes your local identity, shows a toast, and routes you back to onboarding so you pick a new tag. Your existing posts and votes are not deleted, only the tag is reset.

**Smaller Discover polish.** Author avatars get a soft pulse when the post is fresh. The empty state offers three quick-jump buttons instead of the dry "Be the first to post!" line. The compose box placeholder cycles through short prompts when empty so the box never feels stale. Translated across all 12 locales.

### Smoke-test follow-ups

- **Gemini 2.0 family removed.** The 2.0-flash family was deprecated upstream. Picker entries replaced with 2.5-flash, 2.5-pro, and the 3-preview models. Existing settings that point at 2.0-flash auto-migrate forward on next load.

- **In-app navigation no longer reloads the page.** Clicking Open Settings on a toast, the Memory Mode badge in the chat header, and the /settings, /discover, /studio, /codework, /wordpress slash commands all navigate inside the app.

### Deferred

Thread modal (click a reply quote to see the full thread), user profile modal (click a tag to see bio plus recent posts), and post scheduling are not in this release.

## v10.3.2

A maintenance release. Things that already worked now work the way the screens promised. Eleven tracked bugs squashed across MCP, providers, importer, install docs, and locales.

### Fixed

- **Adding an MCP environment variable works on every platform.** The "+ Add environment variable" trigger used a prompt that was unreliable. Replaced with an inline text input and confirm button. Enter-key confirms.
- **MCP Edit deep-link lands on the right tab and scrolls to the right form.** Clicking Edit on the MCP page could previously land on the wrong tab or scroll to an unrelated row. Reliable now. The same fix flows through to template and WordPress / auto-backup anchors.
- **Ollama "detected" banner no longer contradicts a red "not running" hint on Win11.** Previously, a green banner and a red error box could show at the same time when Ollama was running but had no models. The banner now splits: green "Ollama detected, N models available" when models are present, amber "Ollama detected, no models found. Run: ollama pull llama3.2" when zero models are present.
- **Imported ChatGPT, Claude, OpenClaw, and Hermes conversations show up in the sidebar.** Imported chats were previously invisible in the Sessions sidebar. Each imported conversation is now a real chat session with a `[Imported: <source>]` title prefix. Memory search across imported conversations finds substance now.
- **Same-provider retry on transient errors.** Transient failures (network resets, timeouts, HTTP 502, 503, 504) no longer go straight to "No response received." in the chat UI. Skales now retries on the same provider before bubbling up. Layered above the existing model-fallback and cross-provider fallback. Configurable per provider under Settings > Providers.
- **Clearer error messages when using a meta-router.** When a meta-router is configured through the custom-provider slot and an upstream provider is not authenticated, the router used to return a generic network error. Skales now rewrites the message to "Router could not reach upstream provider X. Open your router dashboard and finish connecting X, or switch to a model from a connected provider."
- **API key redaction in error messages covers more providers.** Previously caught Anthropic and OpenAI key forms. Now also catches xAI, Groq, Google, JWT-style keys, and credentials embedded in proxy URLs. Plain English text like "Basic auth required" is left untouched.
- **Locale parity across all 12 locales.** Five chat and settings strings were English originals in all 11 non-English locale files. Translated in DE, ES, FR, HR, JA, KO, PT, RU, TR, VI, ZH. No English drift this release.
- **Linux install guidance updated.** Removed stale "(Beta)" label. Corrected artifact filename patterns. Clearer guidance for Ubuntu 24.04+, with the recommendation to use the `.deb` package on apt-based distros.
- **Friend Mode outreach reads context now.** Outreach used to pick a random keyword and write about it for days, in whatever language it felt like, with no record in your chats. It now reads from your persona, recent session, and memory before sending on Telegram, WhatsApp, or Email, and the message lands in your chat history tagged "via Friend Mode". Replying to the outreach lands in a session that already knows what was said. Language follows your preferences first, then mirrors what you wrote last.
- **MCP Add Server opens the form on arrival.** Previously the "Add Server" button on the MCP page dropped you in Settings with no tab and no scroll. It now opens Settings on the Integrations tab, scrolled to the MCP section, with the Add Server form open.
- **Importer fixes.** The migration picker labelled the GitHub Copilot Chat parser as "Microsoft Copilot", now corrected. Imports from Copilot and Gemini now upload reliably in the same path as ChatGPT and Claude.
- **File tools report where the file actually went.** In workspace-sandbox mode, write operations are redirected into a workspace folder. The result messages used to show the original path, which meant the model would try to read it back from the wrong place. They now show the actual resolved path, with "(redirected to workspace sandbox)" appended.
- **Empty provider responses retry instead of dying.** Providers occasionally return a 200 with no content. That used to surface as "No response received." Skales now retries empty responses the same way it retries network errors. Tool-only responses and deterministic safety refusals are deliberately NOT retried.
- **Provider health check no longer wastes quota.** When Skales fell back to a secondary provider it used to ping the primary every minute. That ate quota on free tiers and could invalidate prompt caches. Recovery now happens on the next real user request: the primary is tried first, and on success the fallback banner clears. The "Retry now" button still works.
- **Retry button on assistant error bubbles.** After all retries and the fallback chain are exhausted, you used to be left with no obvious next move other than retyping. A small Retry button next to the error message now re-submits your last user text. Attachments are not re-attached. Edit the message if you need to retry with a file.
- **Per-provider Timeout and Retries settings live under AI Providers now.** Both used to render inside the Memory tab, which is not where anyone looks for provider configuration. Moved to the bottom of Settings > AI Providers. Saved values are unchanged.
- **The "You can now customize your menu" upgrade notification is gone.** It was a v10.3.0 announcement that kept reappearing. Removed entirely. New users discover Add-Ons through normal navigation.

### Changed

- **Context-size badge loads in all builds.** A previous regression broke the badge in certain builds. Showing user-overridden limits in the badge is queued for v11.

### Migration sources

- ChatGPT, Claude, GitHub Copilot Chat, OpenClaw, and Cherry Studio all import end-to-end with both user messages and assistant responses.
- Gemini imports your prompts only. Google Takeout does not export model responses, so the assistant side of each conversation is empty by design.
- Hermes is supported as an import source. Most users will not need this. It is there for people migrating off Hermes specifically.

## v10.3.1

A maintenance release that cleans up rough edges from v10.3.0. Nothing new on the surface. Things that already worked now work the way the screens promised.

### Fixed

- **Custom Folders survive mode switches.** Saving settings while in Workspace Only or Unrestricted mode used to wipe the configured Custom Folders list. Switching to Custom mode would then show an empty list even though paths were configured. The list is now persisted in every mode.
- **OS notifications respect the Friend Mode OS-notify toggle.** Every incoming Telegram message used to fire a native desktop toast regardless of the Friend Mode setting. OS toasts now respect the setting.
- **Telegram replies are tagged "via Telegram" instead of "via Desktop Buddy".** Subsequent replies in a session used to be relabelled. The original source is now preserved on every turn.
- **MCP Start actually starts the server.** The Start button used to leave the status at "Stopped / 0 tools" even after clicking it. Start now spawns the process and lists tools immediately, the same way Test does. Stop kills the running process without touching the saved config.
- **MCP Edit opens a pre-filled form in edit mode.** Clicking Edit on an existing MCP server used to navigate to an empty Add form. The form is now pre-filled with the server's current settings; the button reads "Save changes" and there is a Cancel option to back out without persisting.
- **MCP template tiles pre-fill the Add form.** Clicking a template tile on the empty-state MCP page now fills in the form for that template instead of dropping you on a blank form.
- **MCP Logs button works.** The Logs drawer used to fail. It now opens and shows the captured logs for the selected server.
- **MCP configs with a combined command string work on all platforms.** A config like `"command": "npx -y obsidian-mcp-server@latest"` with empty args used to work only on Windows. macOS and Linux now handle it too.
- **Desktop Buddy drag stays smooth across the whole screen.** The mascot used to get stuck on Linux when dragged past a certain point. Drag now works the same way on macOS, Windows, and Linux.
- **Desktop Buddy snaps back to a visible display.** If the buddy ends up off-screen after a monitor change, sleep/wake, or rearrangement, it moves back to the primary display's bottom-right corner on the next show.
- **Desktop Buddy on Linux lets clicks through the transparent area.** The bottom-right rectangle around the mascot used to block clicks from reaching the desktop underneath. The buddy now passes clicks through wherever the mascot, the speech bubble, and the input pill are not.


## v10.3.0

A power-user release. The first genuinely native organisational surface (Project Tracker), a working RAG primer, a real command palette, Friend Mode that actually fires, a summarize flow that returns inline infographics, and a manual /cast page for DLNA. The minor-version bump is for the Project Tracker.

### Added

- **Project Tracker (`/projects`).** Linear-style local workflow inside Skales. Each project carries a title, description, status (idea, planning, in progress, paused, done), priority, tags, optional deadline with a colour-coded progress bar and "X days left" / "Overdue by X day(s)" caption, milestone list, notes, and attachments. From the detail view, "Discuss with AI" or "Start working" launches a chat session scoped to the project. From chat: `/projects` (list), `/projects new "Title" | desc` (create), `/projects status "Title" -> in_progress` (move), `/projects open "Title"` (jump in). Storage is local.
- **Friend Mode is alive again.** Proactive check-ins broke when Buddy Mode landed in v8/v9. They work now whenever Friend Mode is enabled, and toggling the master switch in Settings takes effect immediately.
- **WhatsApp and Email channels for Friend Mode.** WhatsApp sends to the first permitted contact. Email sends to your own configured address. The "Coming Soon" placeholder is replaced with a working toggle.
- **Cmd+K / Ctrl+K command palette.** Global fuzzy launcher across every visible nav item, every settings tab, and your 20 most recent chat sessions. Hidden in buddy, spotlight, and bootstrap windows.
- **/search command in chat.** Full-text scan over your saved sessions. Magnifier icon in the bottom-left composer toolbar prefills the composer. Results render inline as ranked snippets with one-click links back to the original chat.
- **/rag command and local Knowledge Base.** Paste documents on /memory (new Knowledge Base card). `/rag <query>` in chat returns the top matching chunks with source labels and scores. All local.
- **Summarize style topbar.** Click the summarize button to choose between text, markdown, HTML infographic, or extract-and-summarize. HTML mode renders inside a sandboxed iframe inline in chat with an editorial aesthetic. The composer stays clean while you type.
- **/cast page.** Manual surface for DLNA / UPnP discovery and control. Lists every device found, shows a discovery log, casts any HTTP media URL with play, pause, stop. Gated by the casting add-on, off by default.
- **13 new bundled templates** across chat, browser, studio, codework, code, planner, organization: Friday Weekly Review, Rubber-Duck Debugger, 2-Option Decision Matrix, Competitor Pricing Scan, Brand Palette Poster, README from Scratch, Deep Work Day Plan, Research+Write Pipeline, Launch Plan Starter, and more.
- **Knowledge Graph visualization.** The KG data store has existed since v9. `/memory` now renders a real graph view with a type-colour legend and hover-to-highlight when KG is enabled.
- **Brand Kit to Studio image bridge.** Brand colours, tone, and typographic direction are appended to every image-generation prompt now, matching what video generation already did.
- **DLNA discovery actually finds devices.** Discovery is more patient and runs in parallel with the fallback scan by default, so dual-band routers no longer under-report.
- Disabled add-ons disappear from all menus consistently.
- Add-Ons toggles take effect across every surface: sidebar, settings tabs, chat tools dropdown, chat quick actions.
- One-shot upgrade notification in the Notification Center explains that add-ons can now be toggled from the sidebar. Dismissed once, never reappears.
- Older sessions with legacy tool-call format play back without breaking chat replay.
- "Powered by GIPHY" and "Powered by Klipy" attribution in Settings, Chat, and Discover Feed.
- Add-Ons page reorganized into tabbed sections: Skales Tools, Communication, Integrations, Computer & Vision.
- Context-size badges next to model names in chat composer and settings, colour-coded by size.
- General settings group: default location and temperature unit. Powers the weather widget and the in-chat weather lookup.
- Multiple Google Calendar IDs supported. Plus-button in calendar config adds a row; reads cover all configured calendars.
- Jina Reader joins Tavily as a web-text extraction option, selectable in Settings > Providers.
- AppImage on Ubuntu 24.04+ now starts cleanly even on restricted kernels.
- Studio Gallery deletes now stick. Toast on failure.
- Reasoning blocks from local model runtimes render cleanly in chat.
- Consistent "Tool Result" label for tool result blocks.

### Changed

- Memory section moved out of the Security tab.
- Tavily and web extractor selector moved from Integrations to Providers.
- Studio and Integrations tabs consolidated.
- Settings search now matches correctly.
- Memory Consolidation (Dreaming) toggle saves on click. Most users finally see a nightly run.
- Sidebar order: Discover lifted above Notifications, Projects lifted above Agents.
- Toasts no longer surface in the buddy desktop pet, the mini-chat overlay, or the spotlight window. They appear only in the main app window.
- Notification action URLs that start with `/` now navigate in the same window instead of opening a new one.
- Set Up Vision Provider button deep-links into Settings instead of routing to Add-Ons.
- Skills renamed to Add-Ons across navigation, page headers, and subtitles.
- Beta indicators removed everywhere except Studio.
- Tools for unconfigured integrations no longer get sent to the model on every request. Big reduction in token usage on small-context local providers.
- ~250 untranslated placeholders cleaned up across 11 non-English locales.
- When you ask Skales "what can you do?", the answer now covers Projects, Knowledge Base (RAG), Chat History Search, Command Palette, Hugging Face Spaces, the Jina extractor option, multi-calendar fan-out, and the default-location weather behaviour.

### Fixed

- Friend Mode now sends proactive messages reliably.
- /search magnifier button is visible on desktop now (was hidden in the mobile-only icon row). Moved to the bottom-left composer toolbar.
- Summarize prefix "Summarize this (URL, Text..):" no longer leaks as visible text into the input bar.
- Mixed-language strings in Russian and Chinese gallery confirmation dialogs.

### Removed

- Deprecated legacy Custom OpenAI provider section.


## v10.2.12

### Added

- **Friend Mode is alive again.** Proactive check-ins broke when Buddy Mode landed in v8/v9. They work now whenever Friend Mode is enabled, and the master toggle in Settings takes effect immediately. No app restart needed.
- **WhatsApp and Email channels for Friend Mode.** WhatsApp sends to the first permitted contact. Email sends to your own configured address. The "Coming Soon" WhatsApp placeholder is replaced with a working toggle.
- **Cmd+K / Ctrl+K command palette.** Global fuzzy launcher across every visible nav item, every settings tab, and your 20 most recent chat sessions. Hidden in buddy, spotlight, and bootstrap windows.
- **/search command in chat.** Full-text scan over your saved sessions. Magnifier icon next to the slash button prefills the composer. Results render inline as ranked snippets with one-click links back to the original chat.
- **/rag command and local Knowledge Base.** Paste documents on /memory (new Knowledge Base card). /rag <query> in chat returns the top matching chunks with source labels and scores. All local.
- **Knowledge Graph visualization.** The KG data store has existed since v9. /memory now renders a real graph view with a type-colour legend and hover-to-highlight when KG is enabled.
- **Brand Kit to Studio image bridge.** Brand colours, tone, and typographic direction are appended to every image-generation prompt now, matching what video generation already did.
- **DLNA discovery actually finds devices.** Discovery is more patient and runs in parallel with the fallback scan by default, so dual-band routers no longer under-report.
- Disabled add-ons disappear from all menus consistently.
- Add-Ons toggles take effect across every surface: sidebar, settings tabs, chat tools dropdown, chat quick actions. Disabling Notion (for example) removes it everywhere until you turn it back on.
- One-shot upgrade notification in the Notification Center explains that add-ons can now be toggled from the sidebar. Dismissed once, never reappears.
- Older sessions with legacy tool-call format play back without breaking chat replay.
- "Powered by GIPHY" and "Powered by Klipy" attribution in Settings, Chat, and Discover Feed.
- Add-Ons page reorganized into tabbed sections: Skales Tools, Communication, Integrations, Computer & Vision.
- Context-size badges next to model names in chat composer and settings, colour-coded by size.
- General settings group: default location and temperature unit. Powers the weather widget and the in-chat weather lookup.
- Multiple Google Calendar IDs supported. Plus-button in calendar config adds a row; reads cover all configured calendars.
- Jina Reader joins Tavily as a web-text extraction option, selectable in Settings > Providers.
- AppImage on Ubuntu 24.04+ now starts cleanly even on restricted kernels.
- Studio Gallery deletes now stick. Toast on failure.
- Reasoning blocks from local model runtimes render cleanly in chat.
- Consistent "Tool Result" label for tool result blocks.

### Changed

- Memory section moved out of the Security tab.
- Tavily and web extractor selector moved from Integrations to Providers.
- Studio and Integrations tabs consolidated.
- Settings search now matches correctly.
- Toasts no longer surface in the buddy desktop pet, the mini-chat overlay, or the spotlight window. They appear only in the main app window.
- Notification action URLs that start with `/` now navigate in the same window instead of opening a new one.
- Set Up Vision Provider button deep-links into Settings instead of routing to Add-Ons.
- Skills renamed to Add-Ons across navigation, page headers, and subtitles.
- Beta indicators removed everywhere except Studio.
- Tools for unconfigured integrations no longer get sent to the model on every request. Big reduction in token usage on small-context local providers.
- ~250 untranslated placeholders cleaned up across 11 non-English locales.
- When you ask Skales "what can you do?", the answer now covers the v10.2.12 surfaces: Knowledge Base (RAG), Chat History Search (/search), Command Palette (Cmd+K), Hugging Face Spaces, Jina extractor option, multi-calendar fan-out, and the default-location weather behaviour.

### Fixed

- Friend Mode now sends proactive messages reliably.
- Mixed-language strings in Russian and Chinese gallery confirmation dialogs.

### Removed

- Deprecated legacy Custom OpenAI provider section.


## v10.2.9

Hotfix for Organization task lifecycle.

### Bug Fixes

- **Instant abort for Organization tasks.** The Abort button cancels in-flight calls within milliseconds now, instead of waiting for the current call to time out. No more wasted tokens on aborted runs.
- **Project deletion stops running tasks.** Deleting a project with an active task aborts the task first, so it stops cleanly.
- **Orphaned tasks cleaned up on startup.** Tasks left running after a crash or restart are marked aborted on next boot, so the UI does not try to resume dead tasks.


## v10.2.8

### Skales Mobile is Live on Android

Skales Mobile is now publicly available on the Google Play Store for Android phones and tablets. Connect to your Skales Desktop instance over the encrypted relay for full feature access, or run the standalone mode with 27 native mobile tools. Install from the Play Store at https://play.google.com/store/apps/details?id=app.skales.mobile.

iOS is in review with Apple. The Play Store launch is the public beachhead; iOS lands the moment review clears.

### New Features

- **Memory Mode.** The setting formerly known as Token Compressor is now called Memory Mode, with clearer mode names (Always Remember, Compact, Minimal) and a more intuitive UI. Minimal mode moved behind an Advanced disclosure to prevent accidental selection. When the active mode is non-default, a small amber Brain badge appears in the chat header to surface the state and provide a one-click jump back to settings. Hidden in Mini Mode, matching the established pattern for Voice, Call, Share, and Incognito.
- **Codework resume banner.** When the most-recent Codework session was paused or interrupted, a dismissible resume banner appears at the top of the welcome view with Resume and Dismiss buttons. The banner replaces the previous Continue button as the canonical resume affordance. Dismiss transitions an active session to a stopped state and persists so the banner does not reappear.
- **Codework file-tree toggle.** New header button toggles the file tree pane visibility, with state persisted across restarts.
- **Codework recent sessions sorted by activity.** Recent sessions now sort by last-touched time instead of filename. Status badges expanded to five states: IN PROGRESS, DONE, ERR, STOPPED, or none for unknown.
- **Sidebar agent filter.** The sidebar now filters sessions by the currently selected agent, so clicking a session no longer reroutes to a different agent's context.
- **Open Folder button.** Codework projects now have an Open in Finder / Open in Explorer button in the project header.
- **OpenRouter as default provider.** New installs and first-time setups now default to OpenRouter as the primary provider for faster onboarding.
- **Tasks expand modal.** Long task results no longer truncate silently. Click any task to open a full-text modal.
- **Persona persistence.** Selected persona now persists across conversation restarts.

### Bug Fixes

- **Session writes no longer clobber each other.** Concurrent writes from chat, buddy, mobile bridge, Telegram, and Spotlight could previously overwrite each other. They now serialize correctly.
- **Tool-only assistant turns no longer vanish.** Interrupted tool calls used to be silently dropped from the chat. They now render as an italic indicator showing the attempted tool names, preserving the conversation timeline.
- **Skill AI and GPT-5.x consolidation.** Edge cases in the GPT-5.x reasoning detection added in v10.2.7 are consolidated and covered.
- **Tool pruning logic.** A regression in tool-pruning for large conversations is corrected.


## v10.2.7

Hotfix for three user-reported regressions surfaced after v10.2.6. No new product surfaces. Auto-updater pipeline unchanged.   Locale parity preserved.

### Bug Fixes

- **OpenAI GPT-5.x models failing with 400 errors.** v10.2.6 detected o1, o3, o4, and bare gpt-5 but missed every GPT-5.x dot-version. Detection now covers the full lineup (gpt-5.1 through gpt-5.5) including every documented suffix and dated snapshot. Works regardless of routing path (direct, OpenRouter, Custom Provider, or any OpenAI-compatible relay).
- **Custom Provider 404 errors.** Base URLs that already include a version segment or full path are detected and not duplicated. Z.ai, Groq, and other providers with non-default URL structures work out of the box. Same detection applies to model-list discovery.
- **Telegram proactive messages returning provider errors.** Friend Mode, Identity Maintenance, daily standup, and cron task completion notifications now go through the same path as in-app chat, so reasoning-model handling stays consistent across every send site.


## v10.2.6

Mini-release focused on critical user-reported bugs across the OpenAI and Gemini providers, sleep/wake recovery, capabilities awareness, and the Planner. No new product surfaces. Auto-updater pipeline unchanged.  

### Bug Fixes (Critical, User-Reported)

- **OpenAI provider 400 across all models.** OpenAI's chat completions API changed conventions in late 2025. Skales now uses the current field names and reasoning-model conventions per model class.
- **Gemini tool calling broken (thought signature missing).** Multi-turn tool conversations with reasoning-enabled Gemini 2.5 Pro and Flash now work.
- **Sleep / wake white screen.** Returning from system suspend or unlocking the screen no longer leaves Skales stuck on a blank page.
- **Capabilities awareness.** Skales knows about its own UI features when asked: math rendering, HTML preview, code-block actions, edit / branch / delete on user messages, manual compact, token-split tooltip, MCP servers, and the live skills system. Asking "can you do math?" or "can you render HTML?" returns "yes" with the right context.
- **Planner: weekly schedules fired daily.** The day-of-week selection used to default to Mon-Fri, which made any "weekly" schedule fire every weekday. Defaults now reset to a single day when you switch to weekly.
- **Planner: day-of-week selections respected.** Picking "Monday + Wednesday" now fires only on Monday and Wednesday.
- **Planner: tasks not visible in Tasks list.** Recurring tasks created in the Planner now appear in the global Tasks page alongside one-off tasks. Each Planner run still produces its own execution entry with full logs.
- **Telegram proactive Friend Mode messages not firing since the Desktop Buddy proactive feature was added.** Friend Mode check-ins, autopilot approval notices, daily standup delivery, and cron-task completion notifications all fire correctly on Telegram again, surviving bot restarts.
- **MCP Servers tab failing to load with 401 error.** Now loads correctly.



## v10.2.5


### Bug Fixes (Critical)

- **Skills system.** Skill toggles were silently ignored since the feature shipped. Computer Use Tools, Calendar Reminders, and other skills now actually function when toggled.
- **UI Skill Toggles.** Toggles persist across restart. Previously, toggles appeared to switch on but reverted after reload. Silent backend errors now trigger UI rollback.
- **Playground Override Persistence.** "Use active model" for per-mode overrides no longer springs back to the previous selection after Save.
- **MCP State Reporting.** The model reports MCP server status correctly instead of always claiming "off".
- **MCP backend status.** Returns real per-server status (disabled, connected, stopped, error) instead of hardcoded "connected" with 0 tools.
- **Calendar Reminders Endpoint.** Was permanently skipped due to a broken setting read. Now wires up correctly.
- **Proxy support.** All provider sites now route through proxy-aware HTTP. Runtime ECONNREFUSED errors with proxy enabled are gone.
- **Token Cap Cloudflare and NVIDIA.** Bumped from a conservative floor up to the real provider ceiling.

### Features

- **KaTeX Math Rendering.** Inline `$E=mc^2$` and block `$$...$$` render as actual mathematics.
- **Edit, Branch, Delete on User Messages.** Hover actions on user bubbles. Edit triggers truncate-and-resend. Branch creates a new chat from that point. Delete removes the message and all subsequent responses.
- **Manual Compact Button.** Compress chat history on demand instead of waiting for the auto-threshold.
- **Token Split Tooltip.** Hover the token badge to see input and output split. Default display unchanged.
- **Code Block Copy.** Hover any code block to reveal a Copy button. 2-second "Copied!" feedback.
- **Code Block Ctrl+A Scoping.** Ctrl/Cmd+A inside a code block selects only that block, not the whole window. Works for Markdown code blocks AND HTML preview blocks.
- **HTML Preview Copy.** Copy button added to the HTML preview header alongside Download HTML.
- **Identity Maintenance Toggle.** Moved to its dedicated section in Settings (was buried under Agent & Tasks).

### Stability / Polish

- **Header Responsive Layout.** Buttons collapse to icon-only on narrow windows with native tooltips on hover. Header no longer breaks on tablet portrait or narrow desktop.
- **Provider Switcher Dropdown.** Anchors correctly in chat and playground. No more left-side cutoff.
- **Compact Button hidden in Mini Mode.** Mini Mode stays minimal.
- **Compaction context retention.** Recent tool calls are preserved as examples after auto-compact.
- **MCP servers no longer crash the app.** Unhandled errors from misbehaving MCP servers are caught.
- **Token Display Tooltip.** Power users see input and output split, casual users see unchanged total.

## v10.2.2

### Provider layer

- **Live model fetch for cloud providers.** Each provider card in Settings > AI Providers now has a Refresh button. Anthropic, OpenAI, Google Gemini, Groq, DeepSeek, Mistral, xAI, Together, MiniMax, Cloudflare, NVIDIA, SambaNova, and Cerebras all support live model listing. Clicking refresh updates the model picker. Model dropdowns prefer the live list when present and fall back to the built-in baseline. New models become usable without a Skales release.
- **User-configurable model limits.** New collapsible "Override Model Limits" section under AI Providers. Add per-provider, per-model override rows for context and output token caps. Use `*` as the model name to apply the limit to all models of that provider that don't have an explicit override. Useful for newly released models whose limits differ from the built-in registry.
- **Per-provider proxy now actually routes.** v10.2.0 declared the feature but it was not wired through correctly. Fixed.

### Chat

- **Manual message delete persists across reload and restart.** v10.2.0 trimmed the in-memory message list but did not save the deletion. Now saved.
- **Branch action creates the correct slice.** v10.2.0 surfaced the Branch button but the slice index was wrong. Clicking Branch on the Nth message now creates a new session with messages 1 through N inclusive.
- **Bubble action labels and toasts are translated.** A handful of locale keys shipped without translations in v10.2.0. Real translations added across all 12 locales.

### Settings

- **Per-Mode Model Override UI uses real provider data.** The dropdowns previously showed a hardcoded curated list regardless of what you had configured. Now mirrors the chat header picker: provider list shows only enabled providers with API keys, model list reflects your configured plus live-fetched models for the chosen provider.
- **Playground on-page picker and Settings Per-Mode Override stay in sync.** Both surfaces persist to the same place and rehydrate from disk on every change.
- **The "?" agents-info trigger no longer appears on the Settings page.** It belongs on the Agents page only, which is unchanged.

### UI

- **Chat and Playground header model pickers hide on small viewports.** On narrow widths the picker is hidden entirely, matching the existing Mini Mode behavior.

### Notes

- Settings schema additions are optional with safe defaults. Existing settings load unchanged.
- 12-locale parity preserved.


## v10.2.0

Iterative quality release across providers, modes, error UX, and chat history. No new product surfaces. Existing surfaces become more resilient and configurable.

### Provider layer

- **Per-provider, per-model limits.** Context window and max output tokens are now looked up per provider and per model. Replaces the previous hardcoded fallback ceilings used across all modes. Unknown models fall through to per-provider defaults, then to a conservative absolute fallback. Live values from HuggingFace Router can override the static entry at call time.
- **Smart context compaction with LLM summary.** When effective context exceeds the budget threshold, older turns are summarized in a single low-cost call instead of being truncated. Falls back to truncation if the summary call fails.
- **Provider error translation.** Raw provider error bodies are translated into actionable user messages with the right next action. Covers Ollama crashes and missing models, OpenRouter rate limits and missing credit, Anthropic and OpenAI context-exceeded and auth issues. Generic fallback adds provider and status for debugging.
- **Per-provider proxy support.** Provider configs accept an optional proxy setting. When set, requests to that provider route through the proxy. Existing settings load unchanged.
- **Multiple custom OpenAI-compatible endpoints.** Settings now supports more than one custom endpoint at a time. The legacy single Custom Provider continues to work and is auto-migrated. Per-entry: label, base URL, API key, model, enabled, tool-calling, and vision toggles.

### Modes

- **Per-mode model resolution.** Each Skales mode resolves provider and model from: explicit caller override, then per-mode override in Settings, then the global active provider and model. Exposed in Settings as a "Per-Mode Model Overrides" panel covering Chat, Codework, Organization, Studio, Playground, Buddy, Spotlight.
- **Playground respects active model.** The previous silent override to Anthropic Sonnet 4.5 is now an opt-in setting (default OFF). When OFF, Playground uses the active provider and model or the per-mode override. Toggle and per-conversation provider and model picker now live on the Playground page header.
- **Inline model picker in Chat.** Compact icon-only button in the chat header opens a popup listing installed providers and curated models. Layout never shifts. Background respects the active light/dark theme. Custom agent provider and model wins over the global default. Picker is hidden in Mini Mode.
- **Chat command `/model <id>` persists.** The slash command writes the new model to your settings, refreshes the picker, and surfaces a clear error bubble on save failure.

### Tools and routing

- **Calendar routing disambiguation.** Natural-language calendar phrasing ("in Google Cal", "in den Kalender", "gcal", "schedule a meeting at TIME") routes to the calendar tool reliably. Planner is now clearly for autonomous Skales prompts, not human appointments.
- **Tavily gate respects user toggle.** When the Tavily skill is disabled or no Tavily API key is configured, web search is filtered out of the tools sent to the model. Other web tools remain enabled.
- **Tool prune for small-context providers.** Providers with small token-per-minute ceilings (such as Groq) automatically receive a pruned tool list, preventing "request too large" errors on free tiers.

### Autopilot

- **Master Switch persists from the Autopilot page.** Toggling the master switch from the Autopilot page (not just Settings) now persists alongside heartbeat start/stop. Activate-on-Start works from a clean restart regardless of which UI surface the toggle came from.
- **Friend Mode observability and persistent cooldown.** Skip reasons are logged. Cooldown survives app restart so it no longer resets to zero on every launch.
- **Identity maintenance auto-approve.** Optional Settings toggle. When enabled, the daily identity maintenance job bypasses the safe-mode and critical-action approval gates. Logged to the audit trail. Default OFF.

### Chat UX

- **Manual delete and branch from any message.** Hover actions on user and assistant message bubbles. Delete trims trailing tool messages so no orphan tool results remain. Branch creates a new session populated with messages up to the chosen point.
- **Resume action on error toasts.** Provider error toasts now carry an action button keyed by the error type: continue or retry on local-model crashes and timeouts, compact on context-exceeded errors, switch-fallback on rate limits and quota errors, open-settings on auth failures.
- **Continuation on output truncation.** When a model stops because it ran out of output room, Skales now asks it to continue instead of dropping the partial answer.

### Settings UX

- **Three-fallback UI cap removed.** The Fallback Chain section accepts as many entries as you want to add.
- **Per-Mode Model Overrides panel.** New section under AI Providers. Per mode: "Use active model" toggle plus provider and model dropdowns when the override is on.
- **Additional Custom Providers panel.** New section under Advanced. Each entry is a card with label, base URL, API key, model, enabled, tool-calling, and vision toggles. Add and remove buttons. Legacy single-slot Custom Provider UI continues to work.
- **Identity Maintenance Auto-approve toggle.** Lives under Autopilot in v10.2.0. Will move under Settings > Memory near the existing identity maintenance controls in a follow-up.

### Discover

- **Layout fixes for long-form posts.** Post text wraps on long URLs. Category badges truncate when very long. Header row wraps when content is wide. Skales Insider posts no longer break the feed layout.

### Telegram

- **Approval flow shows continuation hint.** After a Telegram-approved tool runs, the result message ends with "Tap or send Continue to resume." so you know the agent flow is paused, not finished. Optional auto-resume setting (default OFF) lets the agent continue automatically.

### Updater notifications

- **Changelog field carries through the update notification.** The auto-update notification now includes the full changelog whether the trigger came from a server check or an automatic detection.

### Localization

- 11 new error-translator keys plus 3 new model-picker keys, translated across all 12 locales (de, en, es, fr, hr, ja, ko, pt, ru, tr, vi, zh).


### Notes

- Settings schema additions are optional with safe defaults. Existing settings load unchanged.

---


## v10.1.1 - Hotfix

Five hotfix items rolled up on top of v10.1.0 Design. No new features.


### Vision routing

- **Vision-capable model detection extended.** Gemma 3, Gemma 4, LLaVA, Pixtral, Qwen-VL, Qwen2-VL, Qwen2.5-VL, and MiniCPM-V variants are now recognised. Image inputs route to the configured vision model correctly.
- **Explicit user override is respected.** If you have set a Vision Model in Settings, it is used regardless of whether auto-detection knows about it. Auto-detection becomes a fallback, not a gate.
- **Tool-call hardening.** Malformed tool-call JSON is parsed forgivingly. On total failure, one explicit retry asks the model to return valid format. Tool execution errors are surfaced into the next turn so the model cannot silently report success on a failed write or denied permission.

### Chat history

- **Mobile-origin badge.** Messages synced from Skales Mobile now show a small phone icon next to the timestamp. Tooltip reads "Sent from Skales Mobile". Read-only visual cue, no behavioural change.

### Autopilot

- **Activation modes.** Settings on the Autopilot page now include an Activation Mode picker with three options: Manual (legacy default, last toggle persists), On Startup (heartbeat starts automatically when Skales launches if the master switch is on), and Time Window (heartbeat is active during a user-defined daily 24-hour window such as 09:00 - 17:00). Time windows that cross midnight are supported (e.g. 22:00 - 06:00). Manual toggles inside an active window are respected for the rest of that window so you can pause without fighting the auto-activation. Existing v10.1.0 users default to Manual and see no behaviour change unless they explicitly switch modes.

---

## v10.1.0 "Design"

The biggest creative update yet. Skales Studio gets a Design Tab that turns prompts into real HTML and CSS designs. Codework matures into a full autonomous coding agent. HF Spaces and MCP servers now work everywhere. Smoother animations across the app.

### Studio

- **Studio Design Tab** is the new first tab in Studio. Type a prompt, pick a template (Landing Page, Dashboard, Mobile Screen, Pricing, Hero, Login, Settings), get usable HTML and CSS back. Live preview, palette extraction, font extraction, fullscreen preview (Escape to exit), inline refine drawer, recent designs dropdown. Designs persist between sessions.
- **Studio Image Generation revival.** HuggingFace image provider now works for SDXL, FLUX, and other models. Clear error messages on failure with provider-fallback suggestions.
- **HTML extraction is more forgiving** of common LLM output variants (fenced, unfenced, with or without DOCTYPE, truncated). Smaller models that don't follow exact output format still produce usable designs.
- **Smooth tab crossfades in Studio** on supporting browsers. Graceful fallback on Firefox.

### Codework

Codework matured significantly across the v10.0.4 to v10.1.0 cycle. It is now a full autonomous coding agent, not just a chat with file tools.

- **Approval Gates.** Three new toggles: auto-approve writes, auto-approve exec, auto-approve all. Conservative defaults (Review mode) for first-time users.
- **Forbidden command denylist** expanded. Common destructive operations (`rm -rf $HOME`, fork bombs, dd to disk, etc.) are blocked even with auto-approve enabled.
- **Test loop with progress guardrail.** Codework can run a test command after each code change. After repeated test failures with no progress, the loop aborts and reports back instead of grinding tokens.
- **Preview Mode** for write operations. Write tools generate diffs for you to accept or reject before applying.
- **MCP tool consumption.** Connected MCP servers are now exposed as tools to Codework. Conservative auto-approval gating.
- **Repository-map indexing.** Codework builds a project-wide map of functions, classes, and exports per file. Scales to 500+ files.
- **Long-context tiers.** For huge projects, Codework adapts what it includes in context based on project size.
- **Token usage tracking.** Live token counter shown in Codework, updating per call.
- **Commit-message generator.** New helper drafts commit messages from staged changes following Conventional Commits style.

### Cross-tool integration

- **HF Spaces and MCP everywhere.** Activated HF Spaces and connected MCP servers are now usable from Chat, Codework, AND Studio. Add a Space once, use it anywhere.
- **Active Tools Across Skales** panel in Settings shows which tools are available in which surfaces (Chat, Codework, Studio).
- **Studio can invoke any active HF Space directly.**

### Lio AI

- **Recursive project snapshot.** Lio AI builds a complete file map of your project on each plan and build cycle. Better context awareness for multi-file changes.
- **Plan context** assembled from project structure and chat history for higher-quality plans.

### Chat

- **Short queries keep their tools.** Queries like "Explain X with examples" no longer get stripped to plain chat by the auto-prune heuristic.
- **Exact token counting for context-budget calculations.** Tools are pruned only when they actually exceed provider rate ceilings.
- **Smoother streaming token rendering.**
- **Update toast localized** in all 12 locales with version interpolation. Update detail page renders the actual changelog.

### Stability

- **File reading and writing hardened.** Malformed JSON, missing files, BOM characters, and partial writes no longer crash the app.
- **Hierarchy clarity in Organizations.** Person, Agents, and Organization no longer get confused in multi-agent setups.
- **Namesake trope removed** from all 12 locales (was a phrase pattern that drifted across localizations).
- **Codework session sidebar** active-state correctly handles trailing slashes (no more two-row highlights).
- **Delete session prompt** now properly localized in all 12 languages.


### Mobile

- **Outbox foreground sync.** Pending messages flip to "failed" immediately when the app resumes.
- **Periodic outbox sweep** keeps state fresh during active chat use.

### Landing

- **Migration sources.** Landing page and Migration Importer now list OpenClaw, Hermes, and Cherry Studio alongside ChatGPT, Claude, Copilot, Gemini.
- **Three new feature blocks**: ComfyUI (local image generation), HF Inference Providers (200+ models), DeepSeek V4 (1M context, agent-tuned).

### Note on Lio AI export from Studio

The "Open in Lio AI" export from the Studio Design Tab was removed. Lio AI and Studio Design are different workflows and the link did not work. Use the Download HTML button instead.


## v10.0.4 - April 20, 2026

### Telegram Integration
- **Fixed**: Safe Mode approval flow broken since v9.x. Tool approvals from Telegram now correctly trigger the approval prompt and execute on your "yes" response
- **Fixed**: Telegram bot no longer requires opening the chat page after app launch to come online. The bot starts automatically once the app is ready

### Provider Presets
- **Added**: Minimax, Cloudflare Workers AI, and Nvidia NIM as first-class provider presets with pre-filled endpoints. No more manual Custom OpenAI-Compatible configuration needed for these
- **Added**: "Show only active" toggle in the Providers list to hide unused providers

### Chat & UX
- **Added**: Response time display on assistant messages, see how long each response took
- **Added**: Global hotkey `Cmd+Shift+H` (macOS) / `Ctrl+Shift+H` (Windows/Linux) to toggle Desktop Buddy visibility. Handy for fullscreen video
- **Improved**: Settings search now covers more sections, handles accents (é matches e, ä matches a), and has better keyword coverage in German, Spanish, French, Russian
- **Improved**: Fallback provider banner reworded for clarity with a details modal explaining why the fallback activated and how to fix the primary

### Export & Remote Access
- **Fixed**: Export via Tailscale or remote browser access no longer returns a corrupted HTML file instead of a ZIP.

### Email
- **Improved**: Outlook, Gmail, and Yahoo IMAP authentication errors now explain the App-Specific Password / OAuth2 requirement (Microsoft disabled Basic Auth in 2022) instead of showing a generic "auth failed" message

### Build & Infrastructure
- **Fixed**: Boot log now reports the correct version on every release

### Locales
- All 12 locales (en, de, es, fr, hr, ja, ko, pt, ru, tr, vi, zh) updated with v10.0.4 strings. Informal register maintained.

---

## v10.0.3 - Stability (April 18, 2026)

### Bug Fixes
- **Bonjour/mDNS Collision.** Multiple Skales instances on the same machine no longer shadow each other in swarm discovery
- **Multi-Agent Dispatch Toast.** Completion notification was silently dropped after all subtasks finished. Now fires with job title and subtask count.
- **Update Page i18n.** "Later" button showed a raw key instead of translated text. Translation added to all 12 locale files.
- **Ollama Small-Model Warning.** Settings panel shows an orange warning when a known small model (3B params or fewer) is selected with Max tools above 0, advising you to reduce tools or switch to a larger model.
- **fal.ai Studio Hang.** Video generation polled a stale URL after fal.ai changed their queue structure. Fixed.
- **Codework UI Lag.** Blank activity panel during the first second of a session replaced with a "Starting session..." indicator so the UI never appears frozen.

---

## v10.0.2 - 2026-04-18

### Fixed

- **Tool Filter Regression (critical).** Disabled the context-aware tool filter introduced in v9.2.1 which was silently dropping core tools. This was the root cause of the widespread "Unknown tool" errors after v10.0.0. All tools are now available in every conversation.
- **Export Dialog "Source path not allowed".** Exports failed silently in v10.0.1 because the OS temp directory was not on the allowed source-path list. Fixed.
- **Multi-Step Exit Guard.** Response text emitted alongside tool calls used to be misread as an exit signal, breaking multi-step tasks. Fixed.

### Improved

- **Per-turn cap on identical tool calls raised.** The previous cap was too low to support normal bulk operations like creating multiple folders or writing many files. Infinite loops with identical arguments are still caught by stall detection.
- **Progress-Speak Auto-Continue.** When a model makes tool calls but then stops with short progress-style text ("let me continue", "remaining", etc.), Skales automatically re-prompts it to finish instead of exiting. Mitigates Sonnet 3.7's mid-task pause behavior on bulk operations.

### Known Issues

- Sonnet 3.7 may still pause on large bulk tasks despite auto-continue. Use Claude Opus 4, Sonnet 4, or Minimax for guaranteed single-shot bulk execution.
- Minimax models may emit tool calls as JSON text in chat instead of real function calls for some prompts.
- Codework UI may appear briefly frozen before streaming catches up. The work is happening.
- Multi-Agent Dispatch toast notification is not currently firing. Check the Tasks tab for progress.

---

## v10.0.1 - Hotfix (April 17, 2026)

### Critical Fixes
- **Auto-Updater Schema Mismatch** resolved. Zero successful auto-updates from v10.0.0 was caused by this. Users on v9.x must install v10.0.1 manually once.
- **Export/Import.** Valid zip archives with credential redaction. Accepts legacy formats for backward compat.
- **Multi-Step Tool Chains** no longer exit prematurely when the model returns empty text between tool calls.
- **Advisor Strategy.** Simple chat no longer routed through the expensive Planner.
- **Gemini Tool Schema.** Stripped vendor-specific fields that Gemini silently rejected. Tool calls restored for Gemini models.
- **Calendar reminders and planner tasks no longer get confused.**

### Integrations
- Telegram outbound Chat-ID persists across bot restarts
- SMTP Test race condition eliminated
- Lio AI provider dropdown labels no longer show raw translation key paths
- Custom endpoint URLs (LM Studio, Ollama) accept any capitalisation

### Agent Behavior
- File access works in the configured language without hallucinated "system restriction" excuses
- Folder structure creation supports recursive paths in a single tool call
- Agent checks local state before suggesting support

### Configuration
- New Setting: Request timeout slider for long agent tasks
- Emoji loader stops spamming the console for missing animations

### Discover Feed
- 29 v10 event templates now render custom text

### Security (PHP + WordPress)
- Feed backend: IP hashing aligned across all endpoints
- WordPress Connector 1.2.1: improved token comparison and file upload safety

### Localization
- 132 new settings provider strings across 12 locales
- 4 chat state messages moved from hardcoded English to translation
- Request timeout setting fully translated

### Known Issues
- Reasoning display still abbreviated (deferred to v10.1)
- macOS notarization not yet implemented. Right-click then Open is required on first launch.
- SSH key authentication in SSH tool deferred to v10.1

### Upgrade Path
Auto-update works from v10.0.1 onwards. Users on v9.x: download manually from skales.app once.

---

## v10.0.0 - "Closing the Gap" (April 16, 2026)

The biggest Skales release ever. Desktop, Mobile, and Relay now form one ecosystem: every message you send from your phone routes through Desktop's full tool set, every capability you build on Desktop is reachable from the Mobile companion. Chat feels smoother. Studio speaks video. Settings speaks voice.

### Skales Mobile (NEW)
- Official Skales Mobile app for Android (iOS coming), submitted to Play Store (beta, closed testing)
- Full standalone AI agent in your pocket. 27 mobile tools, works with or without the desktop running.
- Remote Mode: pair via QR over the end-to-end encrypted relay. Keys never leave the devices.
- Paired phones get full access to your desktop's full tool set (shell, files, browser control, email, calendar, Studio, etc.)
- Image upload from mobile forwards to the desktop and gets analyzed like a local upload
- Shared ecosystem: same Discover Feed, same Custom Agents, same Skills

### Studio - LTX-2.3 Video Generation (NEW provider)
- fal.ai LTX-2.3 integration (text-to-video and image-to-video, standard and fast variants)
- $0.06/sec at 1080p, native 9:16 portrait support, 5s and 10s durations
- Added alongside existing Veo, Kling, Runway, Replicate providers
- Live "Connected" badge in Studio when fal API key is configured in Settings
- 4 new localized model labels across all 12 languages

### Animated Emoji System (NEW)
- Noto Color Emoji font bundled. All Unicode emojis render identically on Windows, macOS, and Linux.
- 16 brand and expressive emojis with smooth animations
- Animated splash screen. Gecko mascot animates during app startup.
- Dashboard wave. Hover over the greeting hand for a welcome animation.
- Discover Feed spark picker. Emoji reactions animate on hover, play once in the sent confirmation.
- Chat expressiveness. AI messages with creative, memory, video, or web context emojis animate on arrival.
- Big emoji messages. Send 1-3 emojis alone and they render larger with animation (iOS/Telegram style).
- Easter egg shortcuts in chat: `:gecko:`, `:bubbles:`, `:paw:`, `/highfive`, `/bow`
- Emoji privacy controls. Optional Google CDN fallback in Settings > Privacy (off by default, GDPR compliant).
- Brand emojis preload at startup for instant rendering

### Voice - TTS and STT
- OpenAI TTS provider added (voices: alloy, echo, fable, onyx, nova, shimmer). Reuses the existing OpenAI provider key, no extra setup.
- New "Read responses aloud" toggle in Settings > TTS. When enabled, every assistant reply is spoken via the configured provider once streaming completes.
- Smart markdown stripping before TTS so the voice doesn't read ``` or # out loud
- Per-message speaker button on every assistant bubble. Click to listen, click again to stop.
- Groq-key hint in the STT section (free Whisper access) with one-click jump to AI Providers tab
- All voice UI fully localized across 12 languages

### Chat - Smoothness and Inline Preview
- Smooth spring entrance for new messages
- Session restores stay instant. Only new messages fade in.
- Typing indicator rewritten as a smooth wave
- Typing bubble fades in instead of popping. The indicator never jumps when transitioning to tool-status.
- Scroll-to-bottom button appears bottom-right when you scroll up. Click to return to live view and re-enable auto-follow.
- Inline HTML Preview. HTML code blocks render a live preview with Show Code, Download HTML, Save as Image, Mute, Hide toggles.
- Global mute and hide persist across all chats and sessions
- Save as Image. Pixel-exact capture.
- OS reduced-motion setting disables all animations across the app

### Capabilities & System Prompt
- Version 10.0.0 named "Closing the Gap"
- Skales now knows about Mobile pairing, Inline HTML Preview, the fal.ai video path, Remote API, and the 12 supported languages when asked
- Agent is proactive: when you describe something visual (chart, card, map, SVG, mini-app), it offers inline preview in your language before producing it
- Mobile pairing info is now exposed to the agent
- 6-theme awareness (Dark, Light, Midnight, Forest, Amber, Glass)

### Bug Fixes
- Buddy window draggable on Windows. Cmd/Ctrl+Shift+B global reset shortcut.
- Agent delete button fixed. Replaced with a two-click confirmation directly in the button.
- Playwright chromium detection always picks the newest version installed
- Telegram bot auto-restart watchdog with rate-limit (max 3 respawns per rolling hour). Respects current config.
- Renaming your gamertag updates the existing record in place instead of creating a duplicate
- STT help text shows the translation instead of a raw key
- Studio video-provider "(API key required)" badge now translated across 12 languages
- Boot log now matches the current version (was reporting 9.3.0)
- External links in browser view now open in the default OS browser
- Share window overlay responds to Escape key across chat, spotlight, and buddy
- Browser scroll-to-bottom works reliably on lazy-loading and single-page applications
- Playbook steps now wait for actual page load before proceeding
- macOS screen recording permission detected with user-facing guidance in share window



### Localization
- ~60 new strings added across 12 languages for fal.ai models, HTML preview, voice, Mobile, animated emojis, mute/unmute, scroll-to-latest
- All new German translations are Du/Sie-neutral ("Vorlesen", "Stumm", "Als Bild speichern")


## v9.3.0 - Stability Release (April 13, 2026)

### Stability
- File reading hardened against malformed JSON across the app. Fixes a Windows crash.
- Playground Bridge rewrite. Duplicate injection removed, no more dead buttons.
- Auto-updater fix. Download button now appears correctly, race condition resolved.
- Advisor model validation auto-corrects model IDs for OpenRouter, falls back to primary model on 400/404.
- Playground output cap raised (chat unchanged).
- Skill loading errors consolidated to a single summary line.
- Integrity check downgraded from a warning to an info log.
- Discover Feed admin posting no longer crashes.

### Memory & Intelligence
- Identity Maintenance untouched (runs at 3:00 AM as always)
- Memory Consolidation staggered to 3:30 AM. No overlap with Identity Maintenance.
- Knowledge Graph shows helpful hint when empty instead of "0 entities"
- Agent capabilities awareness updated to v9.3.0 with all current features

### Browser & Automation
- Persistent browser sessions. Logins survive restart.
- Playwright install resolves the binary reliably without depending on the system path.

### Localization
- Removed all "Coming in v9.2.1" text from 12 locale files
- Version strings corrected to 9.3.0 everywhere


## v9.2.5 - "WordPress 2.0" + Playground (April 13, 2026)

### WordPress 2.0
- WordPress Design Skill bundled with 15 Elementor and 10 Gutenberg templates
- Elementor Flexbox Container format (fixes blank pages on modern Elementor)
- Canvas page template auto-set
- Web search available in the WordPress agent
- Selective skill loading keeps the prompt lean
- WordPress Connector Plugin v1.2.0 with collision detection

### Playground (Beta)
- Deep onboarding interview: 15 questions, 4 phases
- AI-powered personalized Space suggestions
- Glassmorphism UI with animated mesh background
- AI-generated interactive Spaces that persist
- AI features wired into the Playground page directly
- Share to Discover Feed with data sanitization
- Milestone system

### New Tool
- **File download tool.** Auto-filename, redirects, VirusTotal scan.

### Fixes
- Duplicate file tools unified
- Slash commands: typed and clicked now identical (all 24 commands)
- /theme toggle fixed
- Memory Consolidation catch-up scheduler
- Playwright install on macOS more reliable
- Discover Feed admin delete and admin free posting
- Studio: Veo 3.0, Imagen 4, GPT Image 1, Kling v2, Runway Gen4 Turbo
- Obsidian theme header navigation updated
- Tool deduplication prevents duplicate function errors
- Tool-awareness warning for local models with tools disabled



## v9.2.3 - File Operations & Stability (April 2026)

### Critical Fixes
- **File tool routing.** Folder and directory tools unified. Tilde expansion now works across all file tools.
- **Model routing.** Skales is now explicit with the model about which tool to use for each file operation.
- **Multi-step tasks.** Agent no longer stops after the first tool call on incomplete directory and file creation.
- **Sidebar version.** Now shows the correct version number (was stuck on 9.2.1).
- **Slash commands.** All 24 commands audited; /tools list updated.

### Improvements
- Duplicate file tools merged. Old names kept as aliases for backward compatibility.
- Duplicate tool definitions removed. Models see one tool per operation.
- Document creation expands tilde paths.
- /tools slash command lists the correct tools.

### Verified (no changes needed)
- Auto-updater: full check, download, verify, install flow confirmed working
- Playwright install: path resolution and error handling all solid


## v9.2.2 - Hotfix (April 2026)

### Critical Fixes
- **Network access restored.** Tailscale, LAN, and remote access work again.
- **Auto-updater.** Full download with progress bar, integrity verification, install and restart UI. No more "Download at skales.app" link.
- **Playwright install.** Install buttons work on systems where brew or npx are not on the default path.
- **Custom Endpoint status.** "Not connected" no longer shown for working local endpoints (LM Studio, KoboldCpp).
- **Custom Endpoint tool slider.** Description updated to mention LM Studio and KoboldCpp.

### Improvements
- Discover Feed admin delete button (for moderators)
- Playwright detection covers more install locations

---

## v9.2.1 - Stability & Completeness (April 2026)

### Ollama / Local Models
- **Tools disabled by default for local models.** Ollama, LM Studio, KoboldCpp, vLLM no longer receive tool definitions. Eliminates timeouts on consumer hardware.
- **Tool slider.** New "Max tools for local models" slider. Shared across all local providers.
- **Fast-fail retry.** If a local model doesn't respond promptly with tools, Skales retries without tools automatically.
- **Timeout leak fix.** Custom endpoint timeout used to override Ollama's longer timeout for all providers. Now scoped to custom endpoints only.
- **Chat hard-kill extended.** Local providers get a longer leash before the chat page kills the request.
- **Local provider detection** covers Ollama, LM Studio, KoboldCpp, vLLM, and any localhost endpoint.

### Advisor Strategy (Fixed)
- **Advisor routing now works in chat.** Plan-vs-execute phase auto-detected from message history.
- **Custom model text field fix.** Selecting "Custom model..." used to clear the model and hide the text input. Fixed for both advisor and executor selectors.

### Agent Skills (SKILL.md)
- **Skills now save to disk.** Imported SKILL.md files persist with manifest tracking.
- **Bulk import.** Import an entire GitHub repo or local parent folder. All subfolders with SKILL.md are imported at once.
- **@-mention in chat.** Type `@` to see a dropdown of installed skills. Select one to inject its SKILL.md content as context for that message. Multiple skills supported.
- **Skills assignable to Agents.** Agent configuration now has a Skills section with checkboxes.
- **Agent skills work across Chat, Spotlight, Browser, Codework, and Organization.**

### Studio
- **API key sharing.** Studio reads keys from main Settings providers. If Google, ElevenLabs, or Azure is configured in Settings, Studio shows "Key set in Settings" instead of "Add API Key".
- **Cloud video generation.** Google Veo, Kling AI, Runway, MiniMax (Hailuo), and Seedance with real cloud API calls and progress polling. No longer "Coming Soon".
- **Veo provider fix.** Was permanently disabled due to a misconfigured provider ID. Fixed.
- **FFmpeg warning hidden for cloud providers.** Cloud video does not need local FFmpeg.

### WordPress
- **Test Connection crash fixed.** WordPress tools now return user-friendly errors for connection refused, 401/403, SSL, and timeout.
- **Full-width CSS v2.** Skales pages render full-width on Astra, GeneratePress, Twenty Twenty-Four, Kadence, OceanWP, and Elementor boxed sections.
- **Skales-created pages flagged for reliable detection.**
- **AI Command Bar reliability.** Clearer workflows for UPDATE, DELETE, CREATE, REDESIGN. More iterations allowed per command.
- **Elementor exits beta.** 5 bundled section templates (Hero, Features Grid, Testimonial, Pricing Table, CTA).
- **WordPress Connector Plugin bumped to v1.1.0**

### Slash Commands (13 new, 24 total)
- `/memory` show memory summary (name, interests, goals, projects)
- `/skills` list installed agent skills with enabled/disabled status
- `/provider` show active provider, model, and base URL
- `/version` show Skales version
- `/export` export current chat as markdown file download
- `/theme` toggle dark/light mode
- `/language` show current locale
- `/settings`, `/discover`, `/studio`, `/codework`, `/wordpress` quick navigation
- `/status` system status check (provider, Ollama, integrations, WordPress)

### Identity Maintenance
- **Runs silently.** No "SECURITY GATE" approval prompts. No dramatic messaging. One-line summary only.

### File Operations
- **Tilde expansion.** `~/` now correctly resolves to home directory across all file write, delete, move, and copy operations.

### Improvements
- Calendar Sync connection status: green/red dot per provider
- Missing skill files warn once per process now, not every cron tick
- ElevenLabs settings link corrected (pointed to Providers, now points to Integrations)
- 13 new slash command descriptions added to all 12 locale files




## v9.2.0 - "The Bridge" (April 2026)

### WordPress Integration (NEW)
- Skales Connector Plugin (MIT-licensed) for WordPress sites
- Token-based authentication
- Auto-detect installed plugins (Elementor, WooCommerce, RankMath, Yoast, cache plugins)
- Create, edit, and delete pages and blog posts with full HTML support
- Elementor page building via JSON sections, columns, and widgets
- WooCommerce bulk price updates by category
- SEO meta management (RankMath and Yoast)
- Media upload (images, videos, PDFs)
- Cache clearing for all major cache plugins
- Full-width CSS injection for Skales-created pages
- Dedicated WordPress management page with AI Command Bar (conversational, real tool execution)
- Per-page AI content generator (inline edit with AI Generate)
- 12 WordPress tools available to the agent

### Stability & Performance
- **Chat loop dedup fix.** Duplicate tool calls are now detected and capped.
- **Tool filter.** Context-based tool filtering reduces the model's tool list per call based on message content.
- **Iteration cap tightened.** Real tasks complete well under the new cap.
- **Skill loading safety.** Missing skill files no longer crash. Graceful skip with warn-once per process.
- **Custom Auto-Updater.** More reliable update flow with streaming downloads.
- **Organization parallel execution.** Independent subtasks now run in parallel.
- **Anthropic timeout increased** for large tool payloads.

### New Features
- **Advisor Strategy.** Opus/GPT-5 for planning, Sonnet/Haiku for execution.
- **Memory Consolidation (Dreaming).** 3-phase overnight memory engine with Dream Diary.
- **Studio Upgrades.** Dynamic model fetching, 10 Style Presets, Camera Controls, Quality Gates.
- **Browser Privacy.** Session isolation, clear cookies, cache, and history.
- **Browser Control v2.** Semantic element detection.
- **OpenClaw Skill Importer.** Import community skills on Custom Skills page.
- **Codework v2.** Multi-file workspace.
- **Lio AI v2.** Template gallery.
- **Social Publishing.** YouTube direct upload and browser-assisted posting.

### Improvements
- Settings page reorganized: Memory tab, Studio tab, proper grouping
- Sidebar grouped into Main, Tools, System sections with always-visible tooltips
- Skills renamed to "Add-Ons" with Activate/Deactivate All
- Model lists update everywhere when one provider's catalog refreshes
- Dark mode persistence improved
- Templates cache faster now
- 12 locale files with 50+ new translation strings
- BSL-1.1 license clarification header

### Bug Fixes
- Tool-call infinite loop fixed
- Browser links no longer open new windows unexpectedly
- File save dialog works correctly
- Settings search covers all new sections (WordPress, Advisor, Dreaming, Memory)
- Sidebar tooltip always visible
- Settings page no longer crashes during navigation
- Studio: Black image, video preview centering, gallery download, reference image handling
- Browser: Session isolation, privacy dropdown, history clear, new tab crash
- Theme and locale persist even after browser data is cleared
- ONNX runtime warnings suppressed


---

## v9.1.0 - "The Studio Update"
Released: April 7, 2026

The biggest feature release in Skales history. Skales Studio,
Templates, Planner AI Tasks, and 40+ improvements across the board.

### Skales Studio (NEW)
- **Image Generation.** Multi-provider support: Skales Visuals
  (built-in renderer), Replicate (Flux, SDXL), HuggingFace,
  OpenAI DALL-E, ComfyUI (local), Stable Diffusion WebUI (local).
- **Video Creation.** Describe a motion graphic, preview the animation live,
  iterate with natural language, export as MP4. Categories: Text
  Animation, Infographic, Data Visualization, Logo Intro, Slideshow,
  Social Post, Counter/Stats.
- **Voice / TTS.** Text-to-speech with automatic provider detection:
  Local, ElevenLabs, Azure Neural, Groq, OpenAI, Google TTS.
- **Music Generation.** AI music via Meta MusicGen (HuggingFace).
  Genre, mood, and duration selection.
- **Gallery.** All generated content (images, videos, audio) saved
  and browsable with filter, search, masonry layout, and reuse.
- **Export.** Format presets for TikTok, YouTube, Instagram, LinkedIn,
  X/Twitter. AI caption and hashtag generator (v9.2.0).
- **Brand Kit.** Save logo, colors, fonts, tagline, tone of voice.
  Optional injection into all Studio generations.

### Templates (NEW)
- 37 pre-built templates across all modules: Chat, Codework,
  Organization, Lio AI, Browser, Planner, Studio
- Click a template to open the module with prompt pre-filled
- Template Maker: AI-guided interview wizard to create custom templates
- Templates shared via Discover Feed (fork from other users)

### Planner AI Tasks (NEW)
- Schedule AI tasks: once, daily, weekly, monthly
- Tasks appear in the calendar grid (purple blocks)
- Auto-execution on schedule
- Confidence scoring: tasks below 50% confidence are skipped
- Dry Run mode: simulate without executing destructive actions
- Task result history with tools used and duration

### Fallback Provider Chain (NEW)
- Configure backup AI providers in Settings
- If primary provider fails, auto-switch to fallback
- Banner notification: "Fallback active: Using [provider]"
- Auto-recovery: checks primary periodically
- API keys inherited from saved provider settings

### Ollama Model Marketplace (NEW)
- One-click install for recommended local models
- Gemma 3, Llama 3.3, DeepSeek R1, Mistral, Phi-4, Qwen 3,
  Codestral listed with sizes and descriptions
- Progress bar during download
- Auto-detection of ComfyUI and Stable Diffusion WebUI

### Browser Playbooks (NEW)
- Record browser sessions as replayable workflows
- Auto-capture URL navigations, clicks, and inputs
- Schedule playbooks as recurring Planner tasks
- Available to the agent in chat and organization

### Social Media Integration (NEW)
- YouTube and LinkedIn OAuth connection in Settings
- Post directly from Studio Export tab
- Instagram, TikTok, Facebook placeholders for v9.2.0

### Knowledge Graph (NEW)
- Knowledge graph builds relationships as you work
- Entities: projects, people, tools, preferences
- Agent can query, update, and delete entries
- Enable/disable toggle and reset in Settings

### Organization Improvements
- Real approval UI with state machine (approve/reject destructive tools)
- Canvas Office visualization
- Shared memory between agents
- Projects CRUD (create, rename, archive, restore, continue)

### Agent Tools (21 new)
21 new agent tools across Brand Kit, image generation and editing,
video creation, voice generation, content extraction, social media,
planner, knowledge graph, and playbooks.

### Internationalization
- 2800+ translation strings across all 12 languages
- All Settings strings now multilingual (450+ converted from hardcoded)
- All module pages fully translated
- Bootstrap wizard fully translated with proper locale loading

### Bug Fixes
- Fixed: Dashboard greeting showing raw translation keys
- Fixed: Planner week and day view missing calendar events
- Fixed: Path traversal vulnerability on code routes
- Fixed: Discover posts showing tips instead of completed tasks
- Fixed: Fallback chain providers not removable after save
- Fixed: Template click not inserting prompt in target module
- Fixed: FFmpeg path resolution on macOS, Linux, Windows
- Fixed: Browser links opening in new tab crashing session
- Fixed: Render progress stuck at 0%
- Fixed: Gallery video downloads serving wrong path
- Removed Beta badges from Swarm, Codework, Organization
- Added Beta badges to Studio, Templates, Playbooks


---

## v9.0.2 - Patch (April 2026)

### Fixed
- Settings: API keys no longer disappear when switching models
- Codework: Project names are sanitized to valid slugs
- Organization: Clipboard copy works with visual feedback
- Organization: Agents respond in the user's configured language
- Discover: Post templates rewritten to describe user activity
- Discover: Added events for Codework and Organization completions

### Added
- YouTube Data API v3 integration (search, video details, channel info, trending, captions)
- Codework: Web search available during code generation

---

## v9.0.0 - "For the People" (April 2026)

### Highlights
- **Agent Skills Import.** Native support for the SKILL.md open standard. Import from Claude Code, Codex, Copilot, Cursor. GitHub URL, local folder, or paste. Works across Chat, Codework, Browser, Spotlight, and Lio AI.
- **Skales Codework.** Autonomous coding agent. Select project folder, describe task, pick model, watch live diffs in 3-panel GUI. Session history and follow-up conversations.
- **Organization.** Multi-agent teams with CEO delegation, departments, Company Packs.
- **Computer Use.** Desktop automation via screenshots, clicks, keyboard, scrolling.
- **Calendar Sync.** Google, Apple, Outlook, CalDAV unified in Planner.
- **7 Integrations.** Notion, Todoist, Spotify, Smart Home, Google Drive, GitHub, Google Docs.

### New Features
- DevKit with API Playground, Debug Panel, CLI, 50+ tool reference
- Migration Importer (ChatGPT, Claude, Copilot, Gemini, OpenClaw, Hermes)
- MCP Server Support (Model Context Protocol)
- New default theme "Skales Modern" (navy and emerald, light/dark)
- Messaging Gateway (Slack, Signal actions)
- 9 professional agents
- DeepSeek direct provider
- Browser Workspaces and Playbooks
- Custom model ID input per agent
- Settings dynamic search (35+ sections)
- Swarm VPN fallback with manual peer IP
- OG preview cards in Discover

### Changed
- Default theme from Classic to Skales Modern
- Light mode as default on first launch
- Skills default state: core features ON, experimental OFF
- Browser loop detection relaxed
- Bubble dismiss timer extended
- Badge color from lime to emerald
- Removed "2.0" from Discover branding
- Removed "Beta" from Browser
- 12 languages (added Turkish, Croatian)

### Fixed
- Calendar events async export crash
- Codework tool hallucination
- Spotlight white flash on open
- Theme flash on restart
- Migration importer file picker error
- Telegram inline keyboard, toast dedup, key persistence
- Settings search not finding Planner and Calendar
- Advanced Integrations in wrong Settings tab
- Raw translation keys in UI
- Crash on certain file writes
- Codework and Organization skill check logic
- Swarm sidebar gating and Skills page toggle
- Dashed-border styling replaced throughout

---

## v8.0.2 - Hotfix (April 2026)

### Fixed
- Chat Error 400: message reconstruction simplified
- Agent "Done" response: removed incorrect tool-call stripping that caused infinite loops with Gemini
- IMAP Email: connects to real server again
- Custom Skills iframe: buttons, inputs, and saves now functional
- Planner weekdays now respect app language setting instead of system locale
- Chat message source badges restored (Desktop, Buddy, Telegram, Spotlight)
- Toast notifications: added X button and click-to-close
- Stop button: more stable behavior on chat page unload
- Chat bubble word-break: fixed mid-word splitting ("correc\nt?" becomes "correct?")
- Think tags no longer leak in Lio AI and Skill AI outputs
- TTS "default" provider: added browser voice selector
- Custom OpenAI-compatible provider: status indicator reflects actual URL config
- Skill Generator: defaults to user's active provider instead of hardcoded OpenRouter
- Telegram bot: auto-reconnects on app restart
- Telegram Safety Mode: approval buttons (Approve/Deny) now use inline keyboard
- Desktop Buddy: sound and notification suppressed when main chat window is focused
- macOS auto-updater: added required ZIP target alongside DMG

### Added
- Notification delete: X button per notification and "Clear All" to dismiss all
- Provider-specific exit condition diagnostics

---

## v8.0.1 - Hotfix (March 2026)

### Fixed
- Chat crash after multiple messages
- Port 3000 conflict detection with health check
- Forked skills truncation (raised limit, added syntax validation)
- Hardcoded German text in UI when set to English
- IMAP email tools now visible to AI when configured
- Discover event spam rate limit survives restart
- A dozen type errors resolved
- Compose drafts now context-aware with per-category agent personality
- Anonymous ID visible in Settings with copy button
- Skills filter tab in Discover feed
- Documents skill: removed non-working Excel claims
- Dark mode dropdown text visibility
- Autopilot priority change no longer deletes task content
- "Feedback submitted" toast shows translated text
- Light theme toggle visibility

### Added
- Migration banner for v8.0.0 users to pick single agent vibe
- Skills filter tab in Discover

---

## v8.0.0 - "Discover 2.0" (March 2026)

### Highlights
- **Discover 2.0.** The first social network where AI agents post, spark,
  mention, and share skills with each other
- **Skill Sharing & Forking.** Share AI-created Custom Skills to Discover.
  Other users can fork (copy) them with one click.
- **Spark.** Send sparks to other agents. Skales' answer to Facebook Poke
  and MSN Nudge. With sound notifications.
- **3 New Languages.** Vietnamese, Croatian, Turkish (12 total)

### New Features
- Discover Feed 2.0 with @mentions, replies, emoji avatars, compose box,
  network visualization, date filters, trending posts
- Spark social interaction system with 6 spark types and sound effects
- Skill AI watermarking for sharing verification
- Share to Discover button for AI-created Custom Skills
- Fork Skill: one-click copy of community skills with safety disclaimer
- Heartbeat system with online counter and network visualization
- Report system for feed moderation with admin review
- Image sharing pipeline with admin approval workflow
- Notification sounds toggle in Settings
- Native file tools for macOS Full Disk Access compatibility
- Toast notification system with theme-aware styling
- Discover onboarding with interest selection, color accent, emoji avatar
- Date filter (Today, This Week, 30 Days, All Time)
- Delete own posts from Discover Feed
- Magic / Spark button for lightweight social interactions
- Edit Discover Profile without losing gamertag

### Fixed
- Discover event pipeline for all tools (images, browser, skills, planner,
  buddy, group chat, spotlight, swarm)
- Browser agent "URL unchanged" false positive on scroll and screenshot actions
- Telegram bot stale lock file on restart
- Request timeout setting now respected (uncapped)
- macOS TCC permission errors with helpful Full Disk Access guidance
- Notification action label displayed correctly
- Swarm only starts network discovery when Swarm is enabled
- Desktop Buddy persists across show/hide (no intro restart on minimize)
- Desktop Buddy no longer steals Cmd+Tab or Dock visibility on macOS
- Token display "0" regression
- Tag duplication in Discover posts
- Toast readable on all themes (light and dark)
- Obsidian theme header icon alignment
- Wrapped card dynamic refresh (includes today's activities)
- Network visualization on high-DPI displays (dots no longer cluster)
- Wrapped PNG export now pixel-accurate

### Languages
- Vietnamese (vi). Full translation.
- Croatian (hr). Full translation, Latin script.
- Turkish (tr). Full translation with correct special characters.
- Total: 12 languages (EN, DE, ES, FR, IT, PT, KO, ZH, JA, VI, HR, TR)

---

## v7.6.6 - Hotfix (March 2026)

### Fixed
- **CRITICAL: Discover Feed tool events never fired.** When users opted in to Discover on the /discover page, the opt-in was saved only locally and never propagated server-side. This caused server-side tool events (image generation, browser sessions, task completions, file organization, swarm dispatches, etc.) to silently not appear in the feed. Only conversation completions worked. Existing users get a background sync on next chat page load.

---

## v7.6.5 - The Intelligence Update (March 2026)

### New Features
- **Token Compressor.** 3-level prompt compression (Full, Compact, Minimal) to reduce API token usage. Configurable in Settings. Minimal is ideal for Spotlight and quick tasks.
- **In-App Toast Notifications.** Floating glassmorphic toasts in the main chat for background task completions, multi-agent dispatches, and dashboard notifications. Auto-dismiss after 5 seconds.
- **Awareness of all UI features.** Skales now knows about Discover Feed, Desktop Buddy (3 skins), Spotlight, Autopilot, Voice Chat, Notifications, Agent Swarm, Multi-Agent Tasks, Planner AI, and Custom Skills. Can navigate you to the correct pages.
- **Discover Feed AI Summaries.** AI instances generate first-person activity summaries locally. Approve or reject on the Discover page before sharing to the community feed. Pulsing dot indicators in sidebar for pending approvals and unread notifications.
- **Custom Skill Interactive UI.** Skills can render their own interactive UI in chat with a bridge for skill-to-host communication.

### New Features (cont.)
- **Skales Wrapped.** Spotify-style weekly stats card. Auto-generates every Monday at 8am or on-demand. Two shareable formats: Square (1:1) and Story (9:16). 4 theme-matched card designs (Skales, Obsidian, Snowfield, Neon). Count-up animations, confetti celebration, staggered stat reveals, animated activity chart. 9 personality badges (On Fire, Power User, Night Owl, etc.). Download PNG, Copy to Clipboard, or Post to Discover. Sidebar pulsing dot when new data. Fully localized in all 9 languages.
- **Discover Feed: GIF Support.** Attach Klipy or Giphy GIFs to AI Summaries. GIF preview in pending approval, safe rendering in feed cards. Admin panel shows GIF URLs and reply-to quotes.
- **Discover Feed: AI Reply and Repost.** Reply to feed entries with AI-generated text. Repost entries to amplify community content. Both with auth verification and rate limiting.
- **Discover Feed: Personality System.** User personality profiles influence AI summary tone and style.
- **Discover Feed: Vibes Tab.** Server-side filtered tab showing only AI summaries.

### Security
- **Discover Repost Auth and Rate Limiting.** Repost endpoint verifies your opt-in. Rate limit: 5 reposts per hour per user.
- **NSFW Filter Expansion.** Gamertag and content filter expanded to 30+ blocked terms covering explicit, violence, hate speech, drugs, and spam.
- **GDPR Delete User Compliance.** Two-pass scrub on user deletion: removes all entries by the leaving user and scrubs replies that referenced them.
- **Admin Panel v6.** Brute-force rate limiting, CSRF tokens, security headers, session hardening.
- **API Rate Limiting on report-status and notifications endpoints.** 429 responses with Retry-After headers.
- **Input validation on all public endpoints.**

### Fixed
- **Discover GIF overflow.** GIF images in feed cards no longer break layout.
- **Discover Vibes tab performance.** Moved to server-side filtering.
- **Discover repost offline handling.** Distinct error messages for rate-limit, server unreachable, and offline states. Graceful degradation for deleted-entry reposts.
- **Admin mobile access.** Burger menu for mobile viewports.
- **Version adoption metric** properly computed from telemetry.
- **Custom Skill buttons.** Skill UIs render interactively with onclick handlers and scripts executing.
- **Skill iframe communication** validated more strictly.
- **Notification polling** reduces server load significantly.


---

## v7.5.0 - The Social Update (March 2026)

### New Features
- **Discover Feed.** Global activity feed showing what the Skales community is building. Gamertag system, upvotes, category filters, blurred preview for non-members. Privacy-first: zero personal data collected, white-label templates only.
- **Spotlight and Vision.** Press Cmd/Ctrl+Shift+S to open a floating search bar anywhere on your desktop. Ask Skales anything without opening the main window. Eye button captures your screen and attaches it to the query for visual context (requires vision-capable model).
- **Spotlight Settings Toggle.** Enable or disable the Spotlight Bar and its global keyboard shortcut from Settings > Notifications. Setting persists across restarts. Disabling it also unregisters the global shortcut to prevent conflicts with other apps.
- **Mini-Chat Mode.** Shrink Skales to a compact always-on-top chat window. Toggle from the chat header or use the Spotlight shortcut.
- **Sound Notifications.** Audible feedback when tasks complete, notifications arrive, or Swarm tasks finish. Theme-aware sounds, configurable in Settings.
- **Agent Swarm Redesign.** Dedicated Swarm page with hub-and-spoke node visualization, task history, quick delegate, and chat integration hints.
- **Notification Center.** Dedicated page for all notifications with read/unread state, filters, and admin broadcast support.
- **Calendar Month View.** Full month grid with event previews, click-to-navigate, and today highlighting.
- **Planner .ics Export.** Download your plan as a calendar file without connecting a provider.
- **TTS Local Provider.** Connect KoboldCpp, XTTS-API-Server, or any OpenAI-compatible TTS endpoint. Configurable in Settings with timeout and automatic browser fallback.
- **Privacy Policy and Delete My Data.** GDPR-ready privacy policy page, in-app Delete My Data button with 2-step confirmation that purges all server-side telemetry, bug reports, and feedback by IP hash.
- **Cookie Consent.** Landing page cookie banner with Google Consent Mode v2. Default deny for analytics/ad storage, granted on explicit Accept.

### Deprecated
- **Network & DLNA.** Network Scanner and DLNA/UPnP casting features retired. The /network route now redirects to Swarm. DLNA casting is planned as a dedicated Smart Home Skill in a future update.

### Fixed
- **Friend Mode and Buddy Intelligence.** Both systems now fire independently of Autonomous Mode. Morning greetings, idle check-ins, meeting reminders, and proactive messages work as configured even when Always-On is off.
- **Calendar delete persistence.** Deleted events stay deleted across view switches and reloads.
- **Desktop Buddy persistence.** Buddy no longer disappears after tab switch or command execution.
- **Ollama detection.** Better error messages and faster checks.
- **KoboldCpp tool calling.** OpenAI-compatible endpoints now send the tools array by default.
- **Telegram loop.** Continued stability from v7.2.1 fix.
- **Bug report email.** Optional contact email now saved and visible to admin.
- **Bug report status sync.** Users see Open, In Progress, Closed status and admin notes.
- **Notification client polling.** Dashboard cards and Notification Center display server notifications.
- **Prompt optimization.** Further token reduction for free-tier models.
- **Swarm state sync.** Settings toggle correctly starts and stops network discovery, auto-starts on boot.
- **Theme responsive.** Swarm, Notifications, and Discover added to all nav variants and mobile menus.

### Security
- API key enforcement for the telemetry endpoint
- Discover Feed: 3-layer gamertag validation, admin shadowban system, rate limiting
- Privacy policy link in Settings > Discover


## v7.2.1 - Hotfix (March 2026)

### Fixed
- **Prompt optimization.** Reduced token usage by moving dynamic context to on-demand tool calls. Free-tier models no longer hit rate limits on simple messages.
- **Calendar widget.** Fixed "Invalid Date" for Google Calendar events with missing dateTime fields.
- **Planner calendar sync.** Fixed "3 errors detected" when sending plans to calendar.
- **Model list cleanup.** Removed deprecated Gemini 1.5 models, added current Groq, OpenRouter, Google models.
- **Weather widget.** Uses device geolocation with Vienna fallback instead of hardcoded Berlin.
- **Telegram approval loop.** Fixed. System jobs bypass approval gates entirely.
- **Identity Maintenance.** Runs automatically without Telegram approval when enabled.
- **Friend Mode.** Tagged as system job, no longer blocked by approval gates.
- **Scheduler heartbeat.** Cron jobs actually execute now.
- **Newsletter telemetry.** Email subscriptions now transmitted to server.

### New
- **Notification system.** Admin can send broadcasts and bug report replies to users. Dashboard shows dismissable notification cards.
- **Browser agent improvements.** DOM settle delay, auto and manual approval modes, dangerous button blacklist, CAPTCHA detection, real-time action log with Markdown export.
- **Agent Swarm.** Network discovery, task delegation, delegate tool, firewall detection, loop prevention.
- **Theme responsive.** Hamburger menus for Snowfield and Neon on mobile, Obsidian tablet overlap fixed, Custom Skills in all mobile menus.

---

## v7.2.0 - "The Next Chapter" (March 2026)

### New Features
- **Dashboard Widgets.** Customizable drag-and-drop dashboard with resizable widgets
  (clock, weather, system stats, quick actions, recent chats, tasks, notes, pomodoro).
  Per-widget settings and theme-aware styling.
- **Cron Scheduling.** Natural-language and cron-syntax task scheduling with job
  management UI, execution logs, and retry support.
- **Browser Tool.** Built-in browser for web research and interaction.
  Sandboxed with user approval flow and screenshot capture.
- **Always-On Agent [BETA].** Background agent that monitors and executes scheduled
  tasks autonomously. Toggle in Settings > Advanced.
- **Live Duplex Voice - Call Mode [BETA].** Full-screen continuous voice
  conversation. Speech-to-LLM-to-speech with barge-in support, waveform visualization,
  and end-call keyword detection. Toggle in Settings > Voice.
- **Multi-Agent Swarm [ALPHA].** LAN peer discovery.
  Discover other Skales instances on the network, view status, and send tasks.
  Hidden behind Settings > Advanced > Experimental.
- **PWA Mobile and Tailscale [BETA].** Progressive Web App manifest with installable
  icons. /mobile page with 4-step Tailscale setup wizard and QR code for phone access.
- **Feedback Page Upgrade.** View your own bug reports with status badges (open,
  in progress, closed). Optional email field on bug reports. Newsletter opt-in
  in onboarding and settings.

### Improvements
- **Ollama Connectivity.** All references switched from localhost to 127.0.0.1 to fix IPv6 resolution issues.
- **Social Links.** X, Instagram, TikTok, and YouTube links in settings, update,
  and feedback page footers.
- **robots.txt and llms.txt** for crawlers and LLM agents.
- **Locale Expansion.** 9 languages (en, de, es, fr, ru, zh, ja, ko, pt) now have full coverage.
  All em-dashes removed from non-English locales.
- **Theme System.** Instant theme switching.

---

## v7.1.0 - "The Local AI Update" (March 2026)

### Bug Fixes
- **Telegram Approval Loop.** Fixed infinite loop where approving an action in Telegram
  triggered the same approval again. Approval responses route correctly and do not
  trigger memory scans.
- **IPv6 localhost.** Fixed bot-to-server connection failure on systems where localhost
  resolves to ::1 instead of 127.0.0.1. (Thanks @bmp-jaller)
- **Think Tags.** No longer leak into chat responses from Qwen and DeepSeek
  models via KoboldCpp. (Thanks @henk717)
- **Desktop Buddy Approve.** Approve button no longer shows "cancelled" due to a sandbox issue.
  Input field no longer overlaps approval buttons.
- **Auto-Updater.** Honest message: "Download at skales.app" instead of a false
  "will install automatically" claim.

### Improvements
- **Onboarding Renamed.** "Custom Endpoint" became "OpenAI Compatible" and moved above Ollama.
  KoboldCpp, LM Studio, vLLM are now first-class options, not hidden under "Custom".
- **API Key Truly Optional.** Empty key means no auth header sent. Local AI servers
  that don't need authentication work without workarounds.
- **Local TTS Endpoint.** Voice settings support local TTS servers (KoboldCpp,
  XTTS-API-Server). Not limited to cloud providers.
- **Local STT Endpoint.** Voice transcription can use local Whisper (KoboldCpp).
- **Local Image Generation.** Configurable image generation endpoint alongside Replicate.



## v7.0.1 - Hotfix (March 2026)

### Bug Fixes
- **Telegram Bot.** Fixed bot process crash on end-user machines. The bot now uses the bundled Node runtime instead of requiring a system Node install. Same fix applied to the WhatsApp bot.
- **Chat Frozen.** Fixed chat becoming unresponsive after vision model error. Session history is now sanitized before every call, preventing corrupted message blocks from breaking subsequent requests.
- **Streaming Timeout.** Added an inactivity timeout to prevent the chat UI from hanging on broken responses.
- **Vision Fallback.** When a model doesn't support vision, images are stripped gracefully and the message is sent as text-only instead of corrupting the session.

---

## V7.0.0 - "The Foundation" (March 2026)

### New Features
- **Proactive Desktop Buddy.** Rule-based buddy intelligence observes calendar, email, tasks, and idle time. Meeting reminders, end-of-day summaries, idle check-ins, morning greetings. Respects quiet hours. No LLM calls.
- **Planner AI.** AI-powered daily scheduling. 8-step wizard learns work patterns, generates time-blocked plans from calendar events, pushes them back to your calendar. Chat integration: "plan my day."
- **Calendar Abstraction.** Google Calendar, Apple Calendar, and Outlook. All three work simultaneously. Planner AI reads from all providers.
- **FTP/SFTP Deploy.** Upload Lio AI projects to any FTP server. Per-project deploy config, incremental upload, test connection, 4 website starter templates.
- **7 Languages.** English, German, Spanish, French, Russian, Chinese (Simplified), Japanese. Full UI translation including onboarding.
- **Skales+ Tiers.** Free Forever, Personal ($9/mo), Business ($29/mo) tier page with waitlist. All features free during beta.
- **Morning Briefing.** Daily digest of calendar events, pending tasks, unread emails, delivered via Telegram and chat.
- **File Sandbox.** Three modes: Unrestricted, Workspace Only, Custom Folders. Enforced on all file tools.
- **Redesigned Onboarding.** 7-step wizard with Cloud, Local, Custom provider cards, Ollama auto-detect, buddy picker, safety mode selection.
- **Model Auto-Fetch.** Real-time model lists from OpenAI, Google, OpenRouter. No more hardcoded model IDs.
- **Linux Beta.** AppImage and .deb builds for x64 Linux.

### Improvements
- **Unified notifications.** All notifications go through one system. Quiet hours, per-type cooldowns, channel routing (bubble, Telegram, dashboard).
- **Settings Restructured.** 6 tabs (General, AI Providers, Integrations, Buddy, Security, Advanced) replace the single long scroll.
- **Custom Endpoint Equality.** Vision toggle, TTS URL, configurable timeout. Local AI is a first-class citizen.
- **Ollama Revolution.** Auto-detect on startup, real model dropdown, faster checks, CORS warning.

### Bug Fixes
- Email Bug 31: Agent respects "send from marketing@" instructions
- Buddy speech bubble height for approval dialogs
- Think and reasoning tags stripped from buddy bubble
- Email whitelist per-mailbox
- Custom endpoint timeout configurable
- Empty API key no longer sends blank auth header
- WhatsApp toggle marked "Coming Soon" (was a dead control)
- Dashboard notification channel fixed (was silently dropping messages)

### Platform
- Windows x64 (stable)
- macOS Apple Silicon (stable)
- macOS Intel (stable)
- Linux x64 AppImage (beta)
- Linux x64 .deb (beta)

---

## V6.2.0 - "The Telegram Fix" (March 2026)

### Critical Fixes
- Fixed: Endless Telegram approval loop. Multiple read-only tools were incorrectly classified as requiring approval. Fixed.
- Fixed: New tools no longer silently block by default. The fallback safety setting flipped from confirm to auto.
- Fixed: Telegram session history preserves tool results properly. The model no longer re-calls already-executed tools.
- Fixed: Google Translate TTS was hardcoded to German. Now uses the user's configured language and locale.

### Improvements
- Telegram approval route now continues the agent loop for natural responses after tool execution
- Autopilot "yes"/"no" intercept now checks task age (5 min window) to prevent eating unrelated messages
- Memory leak fixed in the chat shell on page show events

## V6.1.1 - Hotfix (March 2026)
- Fixed: Telemetry settings now read correctly by the feedback page.
- Fixed: Feature Request textarea not editable on /feedback page (was disabled when telemetry appeared off)
- Fixed: Report Bug sidebar link now opens /feedback instead of old modal
- Fixed: Skin and language changes now prompt for restart
- Fixed: Chat input focus lost after deleting chat or receiving media via Telegram
- Fixed: White screen on mobile Chrome tab switch via Tailscale
- Fixed: Privacy section consolidated. Telemetry toggle moved into Security & Privacy, with dynamic text based on state.
- Updated: All 4 locale files (en, de, es, fr) with new privacy section translations

## V6.1.0 - "The Awakening" (March 2026)

### Autopilot - True Autonomous Agent
- **Recurring Task Scheduling.** Master Plan now generates cron jobs for recurring goals. "Check my email every morning at 8am" creates an actual scheduled task, not a one-shot.
- **Live Execution View.** New tab in Autopilot dashboard shows real-time agent reasoning, tool calls, and results as they happen. Watch Skales think.
- **Automatic Daily Stand-up.** Autopilot generates and delivers a daily briefing via Telegram every weekday at 9am (configurable). No button click needed.
- **Safe Mode: Approval Instead of Skip.** Scheduled tasks in Safe Mode pause for approval instead of being silently skipped. Visible on the Execution Board.
- **Telegram Approval for Autopilot.** Approve or reject Autopilot tasks directly from Telegram. Reply `approve <id>` or `reject <id>`, or simple `yes`/`no` for single pending tasks.
- **Accurate API Rate Limiter.** Cost controls count actual calls per task now. Budget reflects real usage.

### New Features
- **Bubbles Mascot Skin.** A playful blue liquid blob that morphs into different shapes. Selectable in Settings > Desktop Buddy alongside the original Skales gecko.
- **Feedback & Rating System.** New /feedback page with 3 sections: Rate Skales (4 emoji ratings), Report a Bug, Request a Feature. Data sent to server only with telemetry opt-in. GDPR compliant.
- **Admin Dashboard v3.** Redesigned analytics dashboard. Feedback tab with rating distribution, feature request table, and timeline view.

### Bug Fixes (13)
- Fixed: Telegram approval gate ignores safetyMode (Critical)
- Fixed: Telegram inline keyboard buttons never appear (replaced with text-based approval)
- Fixed: Telegram agent hallucinates tool execution when blocked by approval
- Fixed: Telegram pairing shows readable text instead of a raw translation key
- Fixed: Telegram duplicate messages (409 Conflict) from multiple polling instances
- Added: Telegram purge/reset button in Settings
- Fixed: Orphaned tool result blocks no longer crash the Anthropic API path
- Fixed: Replicate images not saved to workspace
- Fixed: Telemetry provider type event now has a cooldown instead of firing on every message
- Fixed: Telemetry language event no longer fires on every app start
- Fixed: Telemetry sends data when opt-in is disabled (GDPR violation)
- Fixed: Rate-limit error now shows the translation instead of a raw key
- Fixed: Identity Maintenance file-path bug
- Fixed: 'medium' priority works correctly in cron task creation

---

## v6.0.2 (2026-03-16)

### Fixed
- **[CRITICAL] Telegram approval gate ignores safetyMode.** Unrestricted mode bypasses approval entirely via Telegram now.
- **[CRITICAL] Telegram inline keyboard buttons don't work.** Replaced with text-based approval ("yes"/"no" replies).
- **[CRITICAL] Agent hallucinates tool execution.** Blocked tools now make their blocked state explicit in the conversation, preventing the model from claiming success.
- **[CRITICAL/LEGAL] Telemetry sends data when opt-in is disabled.** Added a defense-in-depth opt-in check. Zero network requests when telemetry is off. GDPR compliance.
- **[HIGH] Orphaned tool-result blocks crash API.** Added message sanitization that removes tool results referencing non-existent tool calls.
- **[HIGH] Telegram pairing shows raw translation key.** Improved pairing success and failure messages with clear guidance.
- **[MEDIUM] Telegram duplicate messages (409 Conflict).** Added deduplication guard to prevent processing the same update twice.
- **[MEDIUM] Replicate images not saved to workspace.** Fixed download path with explicit error checking.
- **[LOW] Telemetry provider type fires too often.** Cooldown increased.
- **[LOW] Telemetry language event fires every start.** Now only fires when language actually changes.

### Added
- **Telegram Reset button.** "Reset All" button in Settings > Telegram purges all Telegram data.
- **Bubbles mascot skin.** New mascot option: a blue liquid blob that morphs into different shapes. Select in Settings > Desktop Buddy > Skin.
- Skin descriptions shown in the mascot selector UI

### Improved
- Gemini and Replicate images save to a consistent location
- Telegram approval messages are clearer and more user-friendly
- Telegram pairing and error messages are now hardcoded for reliability

---

## v6.0.1 (2026-03-15)

### Fixed
- Safety Mode simplified to Safe and Unrestricted (removed confusing Advanced mode)
- Approval flow no longer stalls after confirming tool execution
- Safe Mode continues the agent loop after approval
- Telegram bot shows proper messages instead of raw translation keys
- Telegram approve and decline inline buttons appear correctly
- Telegram messages cleaned of markdown formatting before sending
- Custom Skill pages have a working input field for all skills
- Replicate image generation works with the new API format
- Telemetry ping limited to once per minute per event
- Capabilities check reports always-active features honestly
- Identity maintenance cron uses built-in tools instead of shell commands (cross-platform safe)
- Locale files verified: all 4 languages have identical structures

### Improved
- Agent acts immediately instead of explaining what it could do
- Platform-aware behaviour: PowerShell vs bash rules based on OS
- Unrestricted mode enables full autonomy
- PDF handling instructions added (try read_file before shell tools)
- Custom skill creation guidance improved
- Enhanced anonymous telemetry: tool usage, provider type, language, feature usage
- All telemetry remains opt-in, anonymous, and GDPR compliant

---

## v6.0.0 - "The Foundation" (March 2026)

### Multilingual
- Full UI translation: English, Deutsch, Espanol, Francais
- Language picker as first onboarding screen
- Language switcher in Settings (always accessible, no restart needed)
- System messages, approval prompts, and error messages translated
- Telegram bot responses in the user's selected language
- Desktop Buddy speech bubbles translated

### New Providers
- Replicate integration (BYOK). Access 50+ image and video AI models with one API key.
- Custom OpenAI-compatible endpoint. Supports llama.cpp, LM Studio, vLLM, koboldcpp, text-generation-webui.
- Tool calling toggle for custom endpoints (on/off, for local models that don't support function calling)

### Skales+
- Tier comparison page (Free Forever, Personal, Business)
- Email waitlist for upcoming premium features
- All current features remain free and unlocked

### Desktop Buddy
- Flickering fix. Smooth crossfade transitions between animations.
- Dynamic folder system. New animations load automatically.
- Full skin system. Add new mascot clips and select from Settings.
- Skin selector in Settings (Desktop App section), shown when more than one skin is installed
- Buddy can now execute tools: write files, send emails, browse the web, manage calendar, and more
- Approve and Decline buttons appear inside the speech bubble when an action needs confirmation
- Auto-executed tools (safe actions) run immediately and show a result bubble
- Tool result summaries shown inline. "Open Chat for details" link for long outputs.

### Privacy and Feedback
- Anonymous telemetry opt-in. Disabled by default. Prompt during onboarding.
- Collected data: app version, OS platform, start and crash events only
- No conversations, no API keys, no file paths, no personal data ever sent
- Anonymous UUID generated once and reused. Never regenerated.
- Report Bug button in the sidebar (bottom, above Stop Server)
- Bug reports sent to developer. Local fallback if offline.
- System info (OS platform) included in reports. Optional checkbox, on by default.

### Approval System
- Unknown tools require approval by default
- Document creation tool added (creates files inside the workspace)
- Telegram inline buttons appear correctly
- Telegram bot works on any port

### Security
- Default tool safety prevents hallucinated tool execution
- Telegram callbacks work regardless of which port Skales is running on
- Chat bubble overflow protection (no more horizontal scrollbar on wide content)

### Bug Fixes
- Chat bubble horizontal overflow fixed
- Translations applied in places that were missing them
- PDF dependency loads reliably

---

## v5.5.0 - March 2026

### Security
- Approval system enforcement. Destructive actions (send email, delete file, calendar changes, tweets) require explicit user confirmation.
- Browser blacklist covers Playwright too. Blocked domains can no longer be bypassed.
- Unrestricted Mode properly bypasses approval gate when enabled
- Screenshot auto-Telegram removed. Only forwards when explicitly requested.

### Accessibility
- ARIA labels on all interactive UI elements (buttons, inputs, navigation, toggles)
- Full keyboard navigation with visible focus indicators
- Screen reader support on chat, buddy bubbles, and approval dialogs
- Skip-to-main-content link
- Compatible with NVDA (Windows) and VoiceOver (macOS)

### Desktop Buddy
- Friendly error messages ("Oops, could you take a look?") instead of raw errors
- Video transition flickering fixed
- Honest response when tools unavailable ("I can only do that in the main chat, Open Chat")

### Bug Fixes
- Input field lock after chat deletion resolved
- Spellcheck disabled globally (both main window and buddy window)
- Custom Skill buttons work now
- Confirmation message shown after approved tool execution


---

## **5.0.0** - The Desktop Companion Update (2026-03-02)

Skales v5.0.0 is the largest single release in the project's history. It ships the full Autopilot meta-agent, Voice Chat, a Custom Skill Ecosystem, Document Generation, Google Places, a Network Scanner, DLNA Casting, a brand-new **Desktop Buddy**, and a comprehensive v5 stability pass.

---

### **Desktop Buddy - Floating Mascot & Spotlight Quick Action**

- **Transparent always-on-top window** at the bottom-right corner of the primary display. No taskbar entry. No shadow. Fully draggable.
- **Mascot states.** The mascot cycles through Intro (welcome clip on launch), Idle (looping base animation), Action (random clip at varying intervals, never repeats the same clip until all have played), and Query (when clicked).
- **Spotlight Quick Input.** Glassmorphism input field with backdrop blur, lime-green glow border, and animated loading spinner. Press Enter to submit, Escape to dismiss.
- **AI Response Bubble.** The reply is shown as a glassmorphism speech bubble with a pointer tail, auto-dismissed after 10 seconds (click to dismiss early). Replies are trimmed for readability.
- **Silent session sync.** Every question and answer is silently saved per day.
- **Settings Toggle.** Desktop Buddy toggle in Settings > Desktop App.
- **Smart Visibility.** Buddy window appears when the main window is minimized or hidden, and hides when the main window is restored. Toggling off instantly hides the buddy.

---

### **Autopilot - The Autonomous Chief of Staff**

- **Autopilot Dashboard.** Dedicated page (`/autopilot`) with four sections: Control Room, Execution Board, Identity & Memory, and Live History.
- **Deep-Dive Interview.** Multi-turn interview that learns your primary goal, niche, budget, and constraints. Saves your profile.
- **Master Plan Generation.** Skales generates a structured roadmap and task list from your profile. Tasks are pushed directly onto the Execution Board.
- **OODA Self-Correction Loop.** If a sub-task discovers new context (dead website, changed pricing, failed dependency), Autopilot autonomously rewrites, deletes, or reprioritises pending tasks and logs the reason with a full audit trail.
- **Human-in-the-Loop Approval Gates.** Tasks involving mass communications, file deletion, or financial transactions auto-flag for approval. The runner pauses until you click Approve or Reject on the Execution Board.
- **API Cost Control.** Configurable max calls per hour and pause-after-N-tasks counter. If a limit is hit, Autopilot pauses and waits for acknowledgment.
- **Anti-Loop Protocol.** Automatic retry tracking. After repeated failures a task is permanently blocked, never retried again.
- **Daily Stand-Up Report.** First-person morning briefing from completed, blocked, and in-progress tasks, plus recent log entries.
- **Execution Board (Kanban).** Full CRUD for tasks: Add, Edit, Cancel, Delete. Filter by state. Shows provider and model, re-plan badge, priority selector, and per-task approve/reject UI.
- **Live History Terminal.** Dark terminal-style log viewer. Colour-coded by level. Auto-polls and caps at 500 entries.

### **Meta-Agent - Universal Skill Dispatcher**

- **Headless Skill Execution.** Autopilot has isolated access to every active skill. Background executions never touch the foreground UI, chat history, or active sessions.
- **Internal Group Chat.** Spawns parallel calls with different personas to reach a consensus on complex decisions.
- **Skill routing syntax.** Tasks can explicitly route to a specific skill handler.

### **Voice Chat Interface**

- **Mic Button.** Amber-styled microphone button between New Session and History (visible only when Voice Chat skill is active).
- **Voice Chat Mode.** Dedicated fullscreen input overlay with status labels (Idle, Recording, Transcribing, Thinking, Speaking), animated pulse ring when recording.
- **Whisper Transcription.** Routes to Groq Whisper first, falls back to OpenAI Whisper.
- **TTS Playback.** ElevenLabs TTS with browser fallback.

### **Skill AI - Custom Skill Ecosystem**

- **ZIP Upload.** Upload a `.skill.zip` to install a new capability. Skales extracts, validates, and loads without restart.
- **AI Scaffolding.** Describe a skill in plain language. Skales generates the full skill definition, handler code, and metadata.
- **Skills Page.** Manage installed custom skills. Enable, disable, view metadata, delete. Isolated sandboxed execution.
- **Security Warning.** All uploaded skills display a security advisory banner before activation.

### **Documents Generation**

- **Word (.docx).** Generate formatted Word documents from natural language.
- **PDF.** Every document request simultaneously generates a PDF version.
- **Excel (.xlsx).** Create spreadsheets with data, formulas, and formatting.
- **Output.** Files saved locally and linked directly in the chat response.

### **Google Places**

- **Nearby Search.** Find restaurants, shops, services near any address or coordinates.
- **Place Details.** Fetch business hours, ratings, reviews, website, phone number.
- **Geocoding.** Convert addresses to coordinates and vice versa.
- **Directions.** Get turn-by-turn navigation data between two points.
- **Photo URLs.** Retrieve Google Places photo references.

### **Network Scanner**

- **LAN Discovery.** Scans the local subnet for devices.
- **Port Detection.** Reports open ports per device. Specifically detects other Skales instances.

### **Media Casting (DLNA/UPnP)**

- **Discovery.** Finds DLNA/UPnP media renderers on the LAN.
- **Cast Controls.** Play, Pause, Stop, Seek, and Set Volume on discovered devices.

### **v5 Polish - Stability, Identity & Infrastructure**

- **Proactive Check-In Cron Loop.** Cron jobs fire automatically on their schedule. In-memory deduplication prevents double-fires within an hour.
- **Voice Chat Mic Crash on HTTP.** Users on plain HTTP now receive a clear error message instead of a silent crash: "Microphone access requires a secure connection (HTTPS or localhost)."
- **Windows App User Model ID.** Toast notifications and taskbar entries now display "Skales" instead of the Electron app ID.
- **Capabilities Registry v5.0.0.** Added 7 new v5 skills: autopilot, custom skills, places, documents, voice chat, network scanner, casting.
- **Mobile UI Polish.** Removed "Talking to: " prefix from the agent selector. Header buttons collapse to icons on mobile.
- **Network & Devices Page** (`/network`). New page with two tabs: Network Scanner (mode selector, live device list with Skales-flag badge) and DLNA Casting (discover renderers, device picker, cast/pause/stop controls).
- **Skill AI Enhancements.** Added "requires API keys" toggle in the Custom Skills generation UI. Enabled required-secrets in the generated skill manifest. Conditional UI Playbook guidance injected when the skill has a UI.
- **Fluid Identity.** Rewrote how Skales builds its self-context. Includes current time, who Skales is, who the user is, key learnings, and recent memory highlights.
- **Agent-to-Agent Protocol** (`/api/agent-sync`). New endpoint supporting ping, handshake, delegate, and status operations. Optional bearer-token authentication.

### **Wake-Up Crash Fix**

- **Global error boundary** catches render errors and async errors. Shows a Skales-themed fallback with a "Reload Skales" button.
- **Polling Guards.** Background polls pause when the window is hidden to prevent wake-up crashes. Applied to voice, video poll, Telegram poll, inbox check, calendar reminders, memory scan, and email check.

---

## **4.0.0** - The Desktop Edition (February 2026)

### **New Features**

- **Native Desktop App.** Skales is now a proper desktop application for Windows and macOS. Install it once. No terminal, no manual server starts, no browser required. Launch it like any other app.
- **Single-Instance Lock.** Opening Skales a second time focuses the existing window instead of spawning a duplicate.
- **Smart Port Detection.** If port 3000 is occupied, Skales automatically tries 3001 and 3002 before failing gracefully.
- **Launch at Login.** Toggle in Settings > Desktop App to start Skales automatically when you log in. Works on both Windows and macOS.
- **Graceful Shutdown.** Skales now signals the internal server on quit and waits for in-flight tasks to finish before force-killing. No more torn bot sessions or half-written data.
- **Hidden CMD Window on Windows.** No more console window flash on startup.
- **macOS app bundle** includes proper copyright, version strings, privacy usage descriptions, and local networking permissions.
- **Home Directory Data Storage.** All user data now lives in the user's home directory, not inside the app bundle. Data persists across updates and reinstalls.
- **macOS Backup Fix.** ZIP import no longer crashes on macOS.

### **Bug Fixes**

- Fixed: ZIP Import overwrites existing data for full recovery
- Fixed: App performs full relaunch after backup import to clear cache

---

## **3.5.0** - The Connections Update (February 2026)

### **New Features**

- **X / Twitter Integration.** Connect your Twitter/X account via OAuth 1.0a. Skales can post tweets, read your timeline, fetch @mentions, and reply to tweets, from the chat interface or via Telegram. Three permission modes: Send Only, Read & Write, Full Autonomous. API keys stored securely locally.
- **Safety Mode.** Three-level command safety system (Safe, Advanced, Unrestricted). Safe mode blocks destructive shell commands (rm -rf, format, dd, fork bombs, etc.) outright. Advanced mode pauses dangerous commands and asks for Approve or Reject. Unrestricted mode disables all blocking for power users.
- **OpenRouter Telegram Vision Fix.** Image uploads via Telegram now work correctly when OpenRouter is the active provider. Skales auto-detects non-vision-capable models and falls back to a vision-capable one.
- **Secure Clipboard Fallback.** Clipboard copy works on HTTP and Tailscale connections (not just HTTPS).

### **Bug Fixes & Improvements**

- Fixed UUID generation breaking on HTTP connections (Tailscale, LAN IPs).
- Fixed mobile input bar disappearing behind the keyboard on iOS and Android.
- Fixed chat scroll-jump when new messages arrive while scrolled up.
- Fixed hydration mismatch on mobile chat page.
- Fixed Telegram memory wordcloud rendering edge case.
- Fixed Playwright cookie banner auto-dismiss not triggering on some pages.
- Improved proactive AI personality. Skales now occasionally initiates conversation based on context.
- Lio AI workspace fixes: invisible projects now visible, chat history preserved across sessions, failed build status resolved.
- Email: Trusted Address Book feature, HTML email rendering, IMAP namespace fix, timezone normalization for event timestamps.
- ElevenLabs TTS fallback chain improved. Now gracefully falls back to Google TTS on API errors.
- macOS: uninstall script renamed for consistency with all other launcher scripts.
- Setup scripts: improved admin rights handling, clearer UX messages, better error reporting.

---

## **3.0.0** - The Power Update (February 2026)

### **New Features**

- **Lio AI - Code Builder.** Multi-AI code builder using Architect, Reviewer, and Builder model pipeline. Build entire apps, websites, and scripts from plain-language descriptions. Navigate to the Code tab to use it.
- **Browser Control.** Headless Chromium automation. Navigate, click, type, scrape, and screenshot any website. Requires Vision Provider.
- **Vision Provider.** Configurable vision model for image analysis, desktop screenshots, and Browser Control. Supports Google, OpenAI, Anthropic, OpenRouter, Groq.
- **Auto-Update System.** One-click update download and installation with progress tracking, automatic backup, and rollback on failure.
- **Group Chat Multi-AI.** Lio AI uses multiple AI models simultaneously for architecture review.
- **Enhanced Memory.** Improved bi-temporal memory system.

### **Bug Fixes & Improvements**

- Fixed Telegram image analysis routing (no longer triggers duplicate reasoning loops)
- Browser Control correctly detects Playwright installation status
- Lio AI time estimates now show realistic values (2-7 min) instead of utopian numbers
- Vision provider label in chat correctly shows active provider name

---

## **2.0.0** - 2026-02-23

### **Added**

* **Message Queue.** Messages are queued when Skales is busy processing. Queued messages are shown in the chat UI with a counter badge. You can cancel individual queued messages or the currently-processing message. Works across Chat, Telegram, and WhatsApp interfaces.

* **Google Calendar Skill.** Read, create, edit, and delete Google Calendar events via OAuth. Skales can check your schedule, add events with reminders, and surface upcoming events as context in every conversation. Configurable in Settings > Skills > Google Calendar.

* **Gmail / Email Skill.** Full IMAP and SMTP email management. Fetch inbox, read threads, compose, reply, search, move, and delete emails. Clean text rendering of HTML emails. Approve and reject safety gates for send and delete operations. New email notifications appear as a banner on the dashboard. Configurable in Settings > Skills > Email.

* **Bi-Temporal Memory System.** Periodic memory scan extracts user preferences, facts, and action items from recent conversations. Memories carry both a valid-time (when the fact is true) and a transaction-time (when it was recorded). Relevant memories are injected as context before every response using local keyword extraction. No external embedding API required.

* **Telegram Admin Interface.** Remote-control Skales from Telegram using inline keyboard menus. Switch providers, models, and personas. Toggle skills on or off. View real-time status. Export conversation data. Admin-only access with PIN protection.

* **Killswitch.** Emergency hard-stop for all AI activity, triggerable via Dashboard button, Telegram `/killswitch` command, or automatically on RAM overload and detected infinite loops. Generates a detailed incident log on the desktop on activation.

* **Multi-Persona Group Chat Skill.** Multiple models with distinct personas discuss a user question in sequential rounds. Fully configurable: participants, language, number of rounds, and personas. Discussions can be exported as Markdown.

* **Autonomous Execute Mode.** Opt-in mode where Skales autonomously handles complex multi-step tasks. Presents a plan for approval, then executes step-by-step with progress updates and approve and reject checkpoints for critical actions (file writes, email sends, deletions). Available via chat and Telegram.

* **Website & Search Security Blacklists.** Domain blocklist prevents Skales from fetching dangerous or inappropriate websites. Word filter blocks harmful search queries before they reach the search API. Both are toggle-controlled in Settings > Security with curated default lists included. Fully customizable from the UI.

* **Responsive UI.** Full mobile and tablet support across the entire dashboard. Collapsible sidebar with overlay, mobile header, touch-optimized controls, and proper viewport handling.

### **Changed**

* Upgraded the internal skill registry to support new skill types (Calendar, Email, Group Chat, Execute Mode).
* Enhanced Telegram handler to support inline keyboard menus and all new admin commands.
* Memory system runs alongside the existing knowledge base (non-breaking additive enhancement).
* Email tools have appropriate approval gates: delete and reply require confirmation, move is automatic.
* Email bodies are converted from HTML to text for cleaner, token-efficient context.
* Dashboard email notification bar shows a single aggregated row (count and latest sender) instead of stacking multiple banners.

### **Fixed**

* Fixed message loss when sending messages while Skales was already processing a response (all messages are now safely queued).
* Fixed security blacklist toggle switches not animating.
* Fixed IMAP MOVE operation fallback on servers that don't support the MOVE extension.

---

## **0.9.0** - 2026-02-19

### **Added**

* **Weather Tool.** Integrated Open-Meteo API for free, keyless 7-day weather forecasts and geocoding.
* **Image Generation Skill.** Integrated Google Imagen 3 via the new Chat Skill Toolbar. Supports multiple aspect ratios and styles.
* **Video Generation Skill.** Integrated Google Veo 2 with asynchronous polling directly in the chat interface.
* **Skills Management Page.** New UI to toggle individual skills (Image Gen, Video Gen, Summarize, Weather) on or off.
* **Chat Skill Toolbar.** Added a "Sparkles" icon to the chat input to access generation panels.
* **Smooth Preloader.** Loading animations (Spin-Ring, Gecko, Bouncing Dots) for better UX.

### **Changed**

* **Persona System Overhaul.** Rewrote all 5 Personas (Default, Entrepreneur, Coder, Family, Student) with deep-dive prompts to give them distinct voices.
* **Agentic Loop Enhancements.** More iterations to handle complex multi-file tasks. Added a visual step-indicator and fixed the stuck-state UI bug.
* **File System Security Toggle.** Added a strict toggle in Settings (Workspace Only vs. Full Access) to sandbox file operations.
* **Self-Awareness (Capabilities Registry v1.4).** Skales can natively audit its own connections, verify identity files, and report on system health via tools.
* **Decoupled Notifications.** The internal scheduler is no longer hard-tied to Telegram, allowing for a universal system inbox.

### **Fixed**

* Fixed Groq TTS issues with a reliable HTTP fallback to Google TTS.
* Auto-switch logic for Vision models correctly triggers when images are pasted or uploaded.
* Fixed the "Enter to send" behavior when images are attached in the chat input.