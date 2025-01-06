# Information Disclosure
### What is information disclosure?

Information disclosure, also known as information leakage, is when a website unintentionally reveals sensitive information to its users. Depending on the context, websites may leak all kinds of information to a potential attacker, including:

- Data about other users, such as usernames or financial information
- Sensitive commercial or business data
- Technical details about the website and its infrastructure

Some basic examples of information disclosure are as follows:

- Revealing the names of hidden directories, their structure, and their contents via a `robots.txt` file or directory listing
- Providing access to source code files via temporary backups
- Explicitly mentioning database table or column names in error messages
- Unnecessarily exposing highly sensitive information, such as credit card details
- Hard-coding API keys, IP addresses, database credentials, and so on in the source code
- Hinting at the existence or absence of resources, usernames, and so on via subtle differences in application behavior
### How do information disclosure vulnerabilities arise?

Information disclosure vulnerabilities can arise in countless different ways, but these can broadly be categorized as follows:

- Failure to remove internal content from public content.
- Insecure configuration of the website and related technologies.
- Flawed design and behavior of the application.

### What is the impact of information disclosure vulnerabilities?

Information disclosure vulnerabilities can have both direct and indirect impacts on websites, depending on the purpose and information an attacker can obtain. Sensitive information can have severe consequences, while technical information, like directory structure or third-party frameworks, may have minimal impact but can be used for exploits.

##### How to assess the severity of information disclosure vulnerabilities

Information disclosure vulnerabilities can be high-severity in specific circumstances, such as when a website uses a known vulnerability. This information is only of interest if it can be exploited by an attacker. It's crucial to focus on the impact and exploitability of leaked information, not just the presence of information disclosure as a standalone issue. However, sensitive information warrants attention in its own right.

### Exploiting information disclosure

##### How to test for information disclosure vulnerabilities

Generally speaking, it is important not to develop "tunnel vision" during testing. In other words, you should avoid focussing too narrowly on a particular vulnerability.

 1. **Fuzzing** : Identify interesting parameters by submitting unexpected data types and fuzz strings. Responses can reveal subtly interesting information, such as processing time, and sometimes the presence of one error case can provide useful information.
 2. **Using Burp Scanner** :
 3. **Using Burp's engagement tools** :
 4. **Engineering informative responses** : Error messages can provide valuable information during testing, but understanding their changes can lead to manipulation of websites to extract data. One method is to make application logic attempt an invalid action on data, resulting in stack trace or debug response with interesting details. Error messages can also reveal desired data values.

### Common sources of information disclosure

* Files for web crawlers
* Directory listings
* Developer comments
* Error messages
* Debugging data
* User account pages
* Backup files
* Insecure configuration
* Version control history

### How to prevent information disclosure vulnerabilities

- Make sure that everyone involved in producing the website is fully aware of what information is considered sensitive. Sometimes seemingly harmless information can be much more useful to an attacker than people realize. Highlighting these dangers can help make sure that sensitive information is handled more securely in general by your organization.
- Audit any code for potential information disclosure as part of your QA or build processes. It should be relatively easy to automate some of the associated tasks, such as stripping developer comments.
- Use generic error messages as much as possible. Don't provide attackers with clues about application behavior unnecessarily.
- Double-check that any debugging or diagnostic features are disabled in the production environment.
- Make sure you fully understand the configuration settings, and security implications, of any third-party technology that you implement. Take the time to investigate and disable any features and settings that you don't actually need.

## References
[1]
PortSwigger, “Information disclosure vulnerabilities | Web Security Academy,” portswigger.net. https://portswigger.net/web-security/information-disclosure

‌