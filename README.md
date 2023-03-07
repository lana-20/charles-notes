# Notes on Charles Proxy


🔵 [Structure Tab Icons]()

🔵 [Exclude a host from being recorded]()

🔵 [Remove a host from a recorded session]()

🔵 [Remove sensitive information from a recorded session]()

🔵 [What happens if Charles root certificate is not installed?]()

🔵 [Remove Charles root certificates]()

🔵 [No internet connection after setting manual proxy]()

🔵 [Miscellaneous issues]()

- <code>Structure</code> tab groups HTTP requests by host.
- <code>Sequence</code> tab shows each HTTP request individually sorted by oldest first.

## Structure Tab Icons

Each host on the Structure tab has one of these four icons (the icons in the program are tiny, hence the  low-res image quality)

<img width="800" src="https://user-images.githubusercontent.com/70295997/223323405-206e3e36-2a8e-4f15-a29b-ab4b6e96a23a.png">

📋 To summarize: lock 🔒 icon means SSL proxying is not enabled for that HTTPS host; lightning ⚡️ in the icon means the host is using HTTP/2 protocol.

## Exclude a host from being recorded

Example scenario: I have Slack Chat open in the background when recording a Charles session and I don't want that to show up in your session.

Solution: go to <code>Proxy > Recording Settings > Exclude > Add</code>.

Let's say I want to exclude <code>xkcd.com</code> and subdomains e.g. <code>imgs.xkcd.com</code>, then I can simply enter <code>*xkcd.com</code> in the **Host** field. For more advanced filters, click **Help** for examples/explanations.


...

Double click on any existing entry to edit it.

Make sure not to exclude any host that is accessed by the website or app under test.

Note: I had issues where hosts that are added to the Exclude list still show up on the session. Interestingly all the problematic ones are HTTPS hosts, whereas the HTTP hosts were excluded without issues. After some time (a few hours? a day?), the issues went away by themselves so I'm not sure what went on there.
## Remove a host from a recorded session



## Remove sensitive information from a recorded session



## What happens if Charles root certificate is not installed?



## Remove Charles root certificates



## No internet connection after setting manual proxy



## Miscellaneous issues



