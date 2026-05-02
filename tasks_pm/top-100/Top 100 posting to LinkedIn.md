Explanation of why the LinkedIn login is set as a condition for displaying the Top 100 page

In a scenario where the user could access the Top 100 page without being logged into LinkedIn beforehand, the process of posting to LinkedIn becomes more complex, requiring an additional state-management flow, extra testing, and introducing a higher risk of edge cases.

The reason is that LinkedIn OAuth login introduces a redirect flow that interrupts the current state of the page.

If the user first selects or modifies the text for sharing and only then clicks “Post to LinkedIn,” they would be redirected to the LinkedIn login page, and after successful authentication, returned back to the Top 100 page.

In this process, it would be necessary to persist the entire state of the user’s action in advance (e.g., via session, local storage, or backend persistence), including which text variant was selected, any manually modified text, as well as the page context from which the share was initiated.

Without an additional mechanism for preserving this state, after returning from the LinkedIn login, the page would be initialized in its default state, meaning the first text variant would be active and any user modifications would be lost.

For this reason, a flow was chosen in which LinkedIn login is required immediately upon page load, as it is simpler and more stable: the user first authenticates via LinkedIn, and only then selects a text variant, optionally modifies it, and posts it to LinkedIn. This approach avoids additional complexity related to storing and restoring temporary user state during the OAuth redirect process.  
