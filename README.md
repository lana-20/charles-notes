**NOTE**: This repo has been refurbushed and published on Medium: https://medium.com/@begunova/charles-proxy-setup-for-desktops-and-mobile-devices-03c3fd28f882.


# Notes on Charles Proxy

🔵 [Structure Tab Icons](https://github.com/lana-20/charles-notes#structure-tab-icons)

🔵 [Exclude a host from being recorded](https://github.com/lana-20/charles-notes#exclude-a-host-from-being-recorded)

🔵 [Remove a host from a recorded session](https://github.com/lana-20/charles-notes#remove-a-host-from-a-recorded-session)

🔵 [Remove sensitive information from a recorded session](https://github.com/lana-20/charles-notes#remove-sensitive-information-from-a-recorded-session)

🔵 [What happens if Charles root certificate is not installed?](https://github.com/lana-20/charles-notes#what-happens-if-charles-root-certificate-is-not-installed)

🔵 [Remove Charles root certificates](https://github.com/lana-20/charles-notes#remove-charles-root-certificates)

🔵 [No internet connection after setting manual proxy](https://github.com/lana-20/charles-notes#no-internet-connection-after-setting-manual-proxy)

🔵 [Miscellaneous issues](https://github.com/lana-20/charles-notes#miscellaneous-issues)

- <code>Structure</code> tab groups HTTP requests by host.
- <code>Sequence</code> tab shows each HTTP request individually sorted by oldest first.

## Structure Tab Icons

Each host on the Structure tab has one of these four icons:

<img width="800" src="https://user-images.githubusercontent.com/70295997/223364085-653d4c6a-5cea-4172-a8e4-66f7467db215.png">

📋 To summarize: lock 🔒 icon means SSL proxying is not enabled for that HTTPS host; lightning ⚡️ in the icon means the host is using HTTP/2 protocol.

## Exclude a host from being recorded

Example scenario: I have Slack Chat open in the background when recording a Charles session and I don't want that to show up in my session.

Solution: go to <code>Proxy > Recording Settings > Exclude > Add</code>.

Let's say I want to exclude <code>xkcd.com</code> and subdomains e.g. <code>imgs.xkcd.com</code>, then I can simply enter <code>*xkcd.com</code> in the **Host** field. For more advanced filters, click **Help** for examples/explanations.

<img width="800" src="https://user-images.githubusercontent.com/70295997/223409076-1287c887-a343-42c2-8a70-66f745e9981a.png">

Double-click on any existing entry to edit it.

Avoid excluding any host that is accessed by the website or app under test (AUT).

📝 I had issues where hosts that are added to the <code>Exclude</code> list still show up on the session. Curiously, all the problematic ones are HTTPS hosts, whereas the HTTP hosts were excluded without issues. After some time (in the range of a few hours, up to about a day), the issues went away by themselves so I'm not sure what happened there.

## Remove a host from a recorded session

Example scenario: a scenario similar to *exclude a host*, except that I didn't add the host in the <code>Exclude</code> list. So the host ended up being recorded in the session. I want to remove that from the session.

Solution: Select the host on the Structure tab, right-click > <code>Clear</code>.

<img width="800" src="https://user-images.githubusercontent.com/70295997/223327698-2dd156c5-f589-47b2-b1ae-99d048d942ac.png">

Avoid accidentally removing any host that is accessed by the website or or app under test (AUT).

## Remove sensitive information from a recorded session

Sometimes I have to use my own account to test an app or website in a cycle. It's important to make sure sensitive information like password is removed or is not present in the recorded session before I upload it as an attachment.

One way is to only start the recording after I log in. That way my login information won't even show up on the recorded session in the first place.

Alternatively, I can press <code>Ctrl+F</code> and search with some keywords like "password". I'll see something like the screenshot below. 

📝 I can right-click on any result and click <code>Remove</code>, but it only removes that result from the search results and not from the recorded session.

<img src="https://user-images.githubusercontent.com/70295997/223346635-7592ac9d-8470-44a8-a85b-d83dc51f6a8f.png" width=800>

Double-click any search result to open up that particular request.

<img src="https://user-images.githubusercontent.com/70295997/223347072-06cdbe9a-8ca7-42da-abbd-ac7025c93d9f.png" width=800>

Once certain that it is the request with the sensitive information, right-click and select <code>Clear</code>.

<img src="https://user-images.githubusercontent.com/70295997/223347252-6abc4411-f78e-4828-a8fe-84ca9535dac1.png" width=800>

Repeat as necessary.

## What happens if Charles root certificate is not installed?

When I have Charles running without having a root certificate installed, most of the sites will browse just fine. But for hosts where I have enabled SSL proxying (by going to <code>Proxy > SSL Proxy Settings...</code> and adding an entry), I'll get an error as seen in the images below.

<img width="1000" src="https://user-images.githubusercontent.com/70295997/223410164-72a58d78-0d91-4b12-9738-018c1c7086f2.png">

<code>Your connection is not private</code> or <code>Did Not Connect: Potential Security Issue</code> error page, as seen on Chrome 110 and Firefox 110.

<img width="1000" src="https://user-images.githubusercontent.com/70295997/223370290-cbd15c07-8d32-4d3a-93d0-d8948b002dbf.png">

## Remove Charles root certificates

#### ✰ Chromium-based browsers
*Tested with Chrome 110*

- [ ] Windows
  - [ ] Open the Run window <code>Win+R</code>, type <code>certmgr.msc</code> and press <code>Enter</code>. If the the root certificate was added under <code>Trusted Root Certification Authorities</code> during the root certificate installation steps, then go there and look for <code>Charles Proxy CA</code> Right-click on it and click <code>Delete</code>.
  
    <img width="800" src="https://user-images.githubusercontent.com/70295997/223412820-0d9426fd-0b55-42bd-af75-a4a5cefc03d3.png">
    
  - [ ] Alternatively, go to <code>Control Panel > Internet Options > Content > Certificates > Trusted Root Certification Authorities</code>, click on <code>Charles Proxy CA</code> and click <code>Remove</code>.

- [ ] macOS
  - [ ] Remove the certificate via the Chrome browser <code>Settings</code> as depicted below:

    <img width="1000" src="https://user-images.githubusercontent.com/70295997/223425947-9e8ab919-7b31-4363-98fe-5de86e2b81ee.png">

  - [ ] Alternatively, go to <code>Spotlight Search > Keychain Access > login > Certificates</code>, click on <code>Charles Proxy CA</code> and click <code>Delete</code>.
    
    <img width="800" src="https://user-images.githubusercontent.com/70295997/223432431-2bc3b421-ddb3-4902-9e11-733560536f56.png">

#### ✰ Firefox
*Tested with Firefox 110*

- [ ] **Windows**
  - [ ] Firefox default directory for certificates is <code>%USERPROFILE%\AppData\Local\Mozilla\Certificates</code> or <code>%USERPROFILE%\AppData\Roaming\Mozilla\Certificates </code> on Windows. Locate the Charles certificate at the path, right-click on it and click <code>Delete or Distrust</code>.
  - [ ] Alternatively, click the navigation drawer menu in the browser's top-right corner and select <code>Settings</code>. Go to <code>Options > Privacy & Security > View Certificates > Authorities tab</code>. Scroll down to <code>XK72Ltd</code>, click <code>Charles Proxy CA</code>, click <code>Delete or Distrust</code> and click <code>OK</code>.
  
    <img width="1000" src="https://user-images.githubusercontent.com/70295997/223414802-09c33ce2-b3d5-4019-ac0a-925972c90994.png">
    
- [ ] **macOS**
  - [ ] [Firefox default directory for certificates](https://support.mozilla.org/en-US/kb/setting-certificate-authorities-firefox) is <code>~/Library/Application Support/Mozilla/Certificates</code> on macOS. Locate the Charles certificate at this path, right-click on it and click <code>Move to Trash</code>.
  
    <img width="600" src="https://user-images.githubusercontent.com/70295997/223615601-4ea52929-2c49-4584-a0f0-972391a0d207.png">

  - [ ] Alternatively, perform removal via the Firefox browser <code>Settings</code>, similar to the Windows flow illustrated above.

    <img width="1000" src="https://user-images.githubusercontent.com/70295997/223579659-867d1a84-7996-4c05-8622-a30d0e0c3d42.png">

#### ✰ Android 13

Go to Settings. Search "certificates" and tap <code>Trusted credentials</code>. Go to <code>User</code> tab and look for root certificate with words like:

    XK72 Ltd.
    Charles Proxy CA

Tap on the certificate and tap <code>Remove</code>.

## No internet connection after setting manual proxy

### Scenario (Windows 10):
I set the manual proxy on my phone to the computer running Charles. When I try to browse a website on the phone, I expect to see a prompt on Charles about an unauthorized device trying to connect, as per the [Charles documentation](https://www.charlesproxy.com/documentation/configuration/access-control/). But I don't see that prompt, and my phone appears to have no internet connection. Even after manually adding the phone's local IP to <code>Proxy > Access Control Settings</code>, there is still no internet access on my phone and Charles is not recording any network activity on the phone.

### Solution:

1. Open Start. Type "network status" and click the matching item.
2. Click <code>Change connection properties</code>.
3. Under <code>Network Profile</code>, select <code>Private</code>(it was originally set to <code>Public</code>).

Charles may need be restarted. Fiddler, however, works fine without having to change the <code>Network Profile</code> to <code>Private</code>

## Miscellaneous issues

❓ Charles is not recording network traffic on Firefox but it is working fine on Chrome and Edge.

👉Go to <code>Options > Settings</code> (under Network Proxy), and make sure **Use system proxy settings** is selected. If I'm getting **Your connection is not secure** on HTTPS sites after that, I may have to visit [https://chls.pro/ssl](https://chls.pro/ssl) and select **Trust this CA to identify websites** to install the SSL certificate on Firefox.

