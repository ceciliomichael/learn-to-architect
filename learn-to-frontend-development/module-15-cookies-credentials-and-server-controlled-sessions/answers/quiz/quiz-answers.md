# Quiz Answers: Cookies, Credentials, and Server-Controlled Sessions

1. **Why prefer HttpOnly session cookies?**

   Browser JavaScript cannot read them, reducing direct token theft through script injection.

2. **What does Secure require?**

   The cookie is sent only over secure transport, subject to browser rules.

3. **What does SameSite help control?**

   Whether cookies accompany certain cross-site requests, reducing some CSRF exposure.

4. **Does a cookie prove authorization?**

   No. The server validates session state and authorization for every protected action.

5. **What does credentials control in fetch?**

   Whether cookies and other credentials are included under the selected origin policy.

