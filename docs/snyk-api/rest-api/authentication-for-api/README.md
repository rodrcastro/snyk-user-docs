# Authentication for API

To use the Snyk API, you must be an Enterprise plan customer and have a token from Snyk.

Enterprise users have [access to a personal token under their profile](./#how-to-obtain-your-personal-token) and to service account tokens. The personal API token is associated with your Snyk Account and not with a specific Organization. Service accounts are associated with an Organization or a Group. For more information, see [Service accounts](../../../enterprise-setup/service-accounts/).

* **Enterprise users should use a service account** to authenticate for any kind of automation. This includes, but is not limited to, CI/CD scanning with the CLI or build system plugins and any automation, including automation with the API.
* **Enterprise users should use the personal token** under their user profile for:
  * Running the CLI locally on their machine; for details, see [Authenticate to use the CLI](../../../snyk-cli/authenticate-to-use-the-cli.md).
  * Authenticating with the IDE manually
  * Running API calls one time, for example, to test something

Note that for free and team plan users, the personal token does not have access to the API and may be used for authenticating to IDE, CLI, and CI/CD integrations only. For details, see [Obtain and use your API token](../../../getting-started/#obtain-and-use-your-snyk-api-token).

For additional information, see [Snyk API token permissions users can control](snyk-api-token-permissions-users-can-control.md).

## How to obtain your personal token

You can find your personal API token in your personal [General Account Settings](https://app.snyk.io/account) after you register with Snyk and log in. In the **key** field, **Click to show**. Then, highlight and copy the API key.

If you want a new API token, select **Revoke & Regenerate.** This will make the previous API token invalid. For details, see [Revoke and regenerate a Snyk API token](revoke-and-regenerate-a-snyk-api-token.md).

## How to use a Snyk API token

When using the API directly, provide the API token in an `Authorization` header, as in the following example request, replacing `API_TOKEN` with your token

```bash
curl --request GET \
--url "https://api.snyk.io/rest/self?version=2024-06-10" \
--header "Content-Type: application/vnd.api+json" \
--header "Authorization: token API_TOKEN"
```

If you are using the API through [Snyk Apps](../../using-specific-snyk-apis/snyk-apps-apis/), provide the `access_token` in an `Authorization` header preceded by `bearer` as follows:

```
Authorization: bearer ACCESS_TOKEN
```

Otherwise, a `401 Unauthorized` response will be returned:

```http
HTTP/1.1 401 Unauthorized

{
    "status": "401",
    "code": "Unauthorized"
}
```

