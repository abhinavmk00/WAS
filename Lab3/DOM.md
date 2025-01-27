## 1. Log the Current URL and Query Parameters

```javascript
// Log the current URL
console.log("Current URL:", window.location.href);

// Extract and log query parameters
const queryParams = new URLSearchParams(window.location.search);
queryParams.forEach((value, key) => {
    console.log(`Query Parameter: ${key} = ${value}`);
});
```

Query parameters can be exploited in phishing attacks by embedding malicious links that look legitimate. For example:  
`https://example.com?redirect=https://malicious-site.com`.  
Attackers use query parameters to redirect users to malicious websites or inject harmful scripts into the URL.

---

## 2. Log Hostname, Protocol, and Pathname

```javascript
console.log("Hostname:", window.location.hostname);
console.log("Protocol:", window.location.protocol);
console.log("Pathname:", window.location.pathname);
```

Attackers might manipulate these properties for malicious redirects by crafting URLs such as `http://fake-example.com/login`. Users could mistake the fake hostname for a legitimate one, falling victim to phishing attacks.

---

## 3. Redirect with a Trusted Domain Check

```javascript
const trustedDomains = ["example.com", "trusted-site.com"];
const targetURL = "https://example.com";

const url = new URL(targetURL);
if (trustedDomains.includes(url.hostname)) {
    window.location.href = targetURL;
} else {
    console.warn("Untrusted domain. Redirect prevented.");
}
```

Open redirects can be exploited by attackers to redirect users to phishing websites. For example:  
`https://legitimate-site.com?redirect=https://malicious-site.com`.

---

## 4. Log Number of Pages Visited

```javascript
console.log("Pages visited in session:", window.history.length);
```

Malicious scripts could exploit browser history to track user behavior or identify sensitive sites visited, leading to privacy violations.

---

## 5. Log User Agent and Identify Browser

```javascript
console.log("User Agent:", window.navigator.userAgent);

if (window.navigator.userAgent.includes("Chrome")) {
    console.log("Browser: Google Chrome");
} else if (window.navigator.userAgent.includes("Firefox")) {
    console.log("Browser: Mozilla Firefox");
} else if (window.navigator.userAgent.includes("HeadlessChrome")) {
    console.log("Browser: Automation Tool");
} else {
    console.log("Browser: Unknown");
}
```

Attackers might use the user agent to detect vulnerabilities in specific browsers or disguise automation tools for malicious activities.

---

## 6. Log Screen Dimensions

```javascript
console.log("Screen Width:", window.screen.width);
console.log("Screen Height:", window.screen.height);
```

Attackers can use screen dimensions to design phishing pages that fit precisely within the user's viewport, making them appear authentic.

---

## 7. Open a Popup Window

```javascript
const popup = window.open("https://example.com", "Example", "width=400,height=400");
if (popup) {
    console.log("Popup opened successfully.");
} else {
    console.warn("Popup blocked by the browser.");
}
```

Popups can be abused to display malicious content or simulate legitimate interfaces. Mitigation strategies include blocking popups and enabling trusted domains only.

---

## 8. Log Domain and Origin

```javascript
console.log("Domain:", window.location.hostname);
console.log("Origin:", window.location.origin);
```

The `origin` property is crucial for Cross-Origin Resource Sharing (CORS). Attackers might exploit improperly configured CORS policies to access sensitive data.

---

## 9. Simulate Login Timeout

```javascript
let timeout;

function resetTimeout() {
    clearTimeout(timeout);
    timeout = setTimeout(() => {
        alert("Session expired due to inactivity.");
    }, 10000); // 10 seconds
}

document.addEventListener("mousemove", resetTimeout);
document.addEventListener("keydown", resetTimeout);

resetTimeout();
```

Timeout functionality enhances security by preventing unauthorized access due to prolonged inactivity.

---

## 10. Check if URL Uses HTTPS

```javascript
if (window.location.protocol !== "https:") {
    alert("This page is not secure. Avoid entering sensitive information.");
}
```

HTTPS ensures encryption of data in transit. Non-secure pages expose users to data theft via man-in-the-middle attacks.

---

## 11. Open and Close a Window

```javascript
const newWindow = window.open("https://example.com", "Example", "width=400,height=400");
if (newWindow) {
    setTimeout(() => newWindow.close(), 3000); // Close after 3 seconds
}
```

Malicious scripts might repeatedly open and close windows to disrupt user experience. Browsers can mitigate this with popup blockers.

---

## 12. Scroll to Top or Specific Element

```javascript
// Scroll to the top
window.scrollTo({ top: 0, behavior: "smooth" });

// Scroll to a specific element
const targetElement = document.getElementById("target");
if (targetElement) {
    targetElement.scrollIntoView({ behavior: "smooth" });
}
```

Attackers might use scrolling to hide malicious overlays or trick users into interacting with invisible elements.

---

## 13. Log and Modify Webpage Title

```javascript
console.log("Current Title:", document.title);

if (!document.title.includes("Secure")) {
    document.title = "Secure - " + document.title;
}
```

Attackers can manipulate the title to mislead users, such as displaying "Your Bank - Login" on phishing sites.

--- 

