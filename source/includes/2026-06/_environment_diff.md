
# Sandbox and Live Environment

Unlike many APIs where the environment is selected by using different endpoints, API keys, or applications, the EasyParcel Open API determines the environment based on the **EasyParcel account** that the user authorizes during the OAuth flow.

## How It Works

The OAuth application (Client ID and Client Secret) is **not tied to a specific environment**. A single application can be used for both Sandbox and Live.

The environment is determined by the EasyParcel account that the user logs in with during authorization.

```text
OAuth Login
      │
      ▼
User logs in with EasyParcel Account
      │
      ├──────── Sandbox Account ────────► Sandbox Environment
      │
      └──────── Live Account ────────► Live Environment
```

<img width="100%" src="https://github.com/user-attachments/assets/d67b1c05-217c-41d9-a5a7-e9d30bfe9cb5" />


## Environment Mapping

| Authorized Account Type | API Environment |
| ----------------------- | --------------- |
| Sandbox Account | Sandbox |
| Live Account | Live |

This means:

- If the user authorizes using a **Sandbox Account**, all API requests made with the resulting access token will be processed in the **Sandbox** environment.
- If the user authorizes using a **Live Account**, all API requests made with the resulting access token will be processed in the **Live** environment.

## Do I Need Separate Applications?

**No.**

You can use the same OAuth application (Client ID and Client Secret) for both Sandbox and Live.

For example:

| OAuth Application | Authorized Account | Environment |
| ----------------- | ------------------ | ----------- |
| My Integration | Sandbox Account | Sandbox |
| My Integration | Live Account | Live |

There is no need to create separate applications for different environments unless you want to manage them separately for your own purposes.

## How Do I Switch from Sandbox to Live?

If you previously authorized a **Sandbox Account**, the access token will only work with the Sandbox environment.

To switch to Live:

1. Log out (or revoke the existing authorization if applicable).
2. Start the OAuth authorization flow again.
3. Sign in with your **Live EasyParcel account**.
4. Obtain a new access token.

The newly issued access token will automatically access the Live environment.

> Existing access tokens cannot be converted from Sandbox to Live. A new OAuth authorization must be completed using a Live account.

## Frequently Asked Questions

### Do I need different Client IDs for Sandbox and Live?

No. One OAuth application can be used for both environments.

### Do I need different API endpoints?

No. The same OAuth flow and API endpoints are used. The environment is determined by the authorized EasyParcel account.

### Can I use a Sandbox access token to call the Live environment?

No. An access token is tied to the account that authorized it. If it was issued by a Sandbox account, it can only access the Sandbox environment.

### Can my application support both Sandbox and Live users?

Yes. Your application can support both environments simultaneously. Simply have each user authorize using the appropriate EasyParcel account:

- Sandbox account → Sandbox
- Live account → Live

Each authorization will return an access token that is associated with the corresponding environment.
