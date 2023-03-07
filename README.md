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

Each host on the Structure tab has one of these four icons:

<img width="800" src="https://user-images.githubusercontent.com/70295997/223364085-653d4c6a-5cea-4172-a8e4-66f7467db215.png">

📋 To summarize: lock 🔒 icon means SSL proxying is not enabled for that HTTPS host; lightning ⚡️ in the icon means the host is using HTTP/2 protocol.

## Exclude a host from being recorded

Example scenario: I have Slack Chat open in the background when recording a Charles session and I don't want that to show up in your session.

Solution: go to <code>Proxy > Recording Settings > Exclude > Add</code>.

Let's say I want to exclude <code>xkcd.com</code> and subdomains e.g. <code>imgs.xkcd.com</code>, then I can simply enter <code>*xkcd.com</code> in the **Host** field. For more advanced filters, click **Help** for examples/explanations.

<img width="800" src="https://user-images.githubusercontent.com/70295997/223326969-43cc76a9-2aca-4432-ab2c-09b490f47b67.png">

Double click on any existing entry to edit it.

Make sure not to exclude any host that is accessed by the website or app under test (AUT).

Note: I had issues where hosts that are added to the <code>Exclude</code> list still show up on the session. Interestingly, all the problematic ones are HTTPS hosts, whereas the HTTP hosts were excluded without issues. After some time (a few hours? a day?), the issues went away by themselves so I'm not sure what went on there.

## Remove a host from a recorded session

Example scenario: a scenario similar to *exclude a host*, except that I didn't add the host in the <code>Exclude</code> list. So the host ended up being recorded in the session. I want to remove that from the session.

Solution: Select the host on the Structure tab, right-click > <code>Clear</code>.

<img width="800" src="https://user-images.githubusercontent.com/70295997/223327698-2dd156c5-f589-47b2-b1ae-99d048d942ac.png">

Make sure not to accidentally remove any host that is accessed by the website or or app under test (AUT).

## Remove sensitive information from a recorded session

Sometimes I have to use my own account to test an app or website in a cycle. It's important to make sure sensitive information like password is removed or is not present in the recorded session before I upload it as an attachment.

One way is to only start the recording after I log in. That way my login information won't even show up on the recorded session in the first place.

Alternatively, I can press <code>Ctrl+F</code> and search with some keywords like "password". I'll see something like the screenshot below. Note: I can right click on any result and click <code>Remove</code>, but it only removes that result from the search results and not from the recorded session.

<img src="https://user-images.githubusercontent.com/70295997/223346635-7592ac9d-8470-44a8-a85b-d83dc51f6a8f.png" width=800>

Double-click any search result to open up that particular request.

<img src="https://user-images.githubusercontent.com/70295997/223347072-06cdbe9a-8ca7-42da-abbd-ac7025c93d9f.png" width=800>

Once certain that it is the request with the sensitive information, right-click and select <code>Clear</code>.

<img src="https://user-images.githubusercontent.com/70295997/223347252-6abc4411-f78e-4828-a8fe-84ca9535dac1.png" width=800>

Repeat as necessary.

## What happens if Charles root certificate is not installed?

When I have Charles running and I didn't install its root certificates, most of the sites will browse just fine. But for hosts where I have enabled SSL proxying (by going to <code>Proxy > SSL Proxy Settings...</code> and adding an entry), I'll get an error as seen in the images below.

<img width="1000" src="https://user-images.githubusercontent.com/70295997/223360167-06a80fa0-9754-4ddf-9f26-eb555d31cc82.png">

<code>Your connection is not private</code> or <code>Your connection is not secure</code> error page, as seen on Chrome 110 and Firefox 110.

<img width="1000" src="https://user-images.githubusercontent.com/70295997/223370290-cbd15c07-8d32-4d3a-93d0-d8948b002dbf.png">

## Remove Charles root certificates



## No internet connection after setting manual proxy



## Miscellaneous issues

❓ Charles is not recording network traffic on Firefox but it is working fine on Chrome and Edge.

👉Go to <code>Options > Settings</code> (under Network Proxy), and make sure **Use system proxy settings** is selected. If I'm getting **Your connection is not secure** on HTTPS sites after that, I may have to visit [https://chls.pro/ssl](https://chls.pro/ssl) and select **Trust this CA to identify websites** to install the SSL certificate on Firefox.

