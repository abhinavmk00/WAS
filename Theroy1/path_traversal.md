# Path Traversal

Path traversal is also known as directory traversal.

#### What is path traversal ?
These vulnerabilities enable an attacker to read arbitrary files on the server that is running an application.
#### Reading arbitrary files via path traversal
For example:

`https://insecure-website.com/loadImage?filename=218.png`

at the backend gets the file

`/var/www/images/218.png`

so if we send a request like

`https://insecure-website.com/loadImage?filename=../../../etc/passwd`

at the backend it gets the file

`/var/www/images/../../../etc/passwd`

which is equavalnet to 

`/etc/passwd`

or the equvalnet for windows backend server

`https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini`

#### Common obstacles to exploiting path traversal vulnerabilities
Many applications that place user input into file paths implement defenses against path traversal attacks. These can often be bypassed.
###### File path traversal, traversal sequences blocked with absolute path bypass
You might be able to use an absolute path from the filesystem root, such as `filename=/etc/passwd`
###### File path traversal, traversal sequences stripped non-recursively 
You might be able to use nested traversal sequences, such as `....//` or `....\/`
###### File path traversal, traversal sequences stripped with superfluous URL-decode
You can sometimes bypass this kind of sanitization by URL encoding, or even double URL encoding, the `../` characters. This results in `%2e%2e%2f`
##### File path traversal, validation of start of path
An application may require the user-supplied filename to start with the expected base folder, such as `/var/www/images`. In this case, it might be possible to include the required base folder followed by suitable traversal sequences. For example: `filename=/var/www/images/../../../etc/passwd`
##### File path traversal, validation of file extension with null byte bypass
An application may require the user-supplied filename to end with an expected file extension, such as `.png`. In this case, it might be possible to use a null byte to effectively terminate the file path before the required extension. For example: `filename=../../../etc/passwd%00.png`.
#### How to prevent a path traversal attack
The most effective way to prevent path traversal vulnerabilities is to avoid passing user-supplied input to filesystem APIs altogether.

If you can't avoid passing user-supplied input to filesystem APIs, we recommend using two layers of defense to prevent attacks:
- Validate the user input before processing it. Ideally, compare the user input with a whitelist of permitted values. If that isn't possible, verify that the input contains only permitted content, such as alphanumeric characters only.
- After validating the supplied input, append the input to the base directory and use a platform filesystem API to canonicalize the path. Verify that the canonicalized path starts with the expected base directory.

## References
[1]
PortSwigger, “What is directory traversal, and how to prevent it?,” Portswigger.net, 2019. https://portswigger.net/web-security/file-path-traversal