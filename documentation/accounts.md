# Accounts

Accounts are the main page for managing your customers. The account object stores the entire Recurly history of your customer and acts as the entry point for working with a customer's billing information, subscription data, transactions, invoices and more.

![Accounts Management ](../.gitbook/assets/screenshot-20200521163151-1559x929%20%282%29.png)



## Account Status

During its existence account can be involved in different event that can change its status. For example end of trial period or problems with payment status. This article describes account statuses that can be seen by users.

![Account statuses transition scheme.](../.gitbook/assets/end-company-statuses-lifecycle%20%282%29.svg)

### Statuses descriptions

`created` - account was just created and registration process is not finished yet.

`trial` - if billing plan defines trial period account will enter in trial period.

`active` - account enter in active status in next cases:

* billing plan defines no trial and account have disabled payments.
* billing plan defined no trial and account should't provide payment method during registration.
* billing plan defined no trial and account must provide and provided valid payment method.
* trial ended and account have disabled payments.
* trial ended and account should't provide payment method during registration.
* trial ended and account must provide and provided valid.
* account payment subscription returned to active state.

`suspended` - account have problems with payments.

### Account Subscription 

![](../.gitbook/assets/image%20%2862%29.png)

### Change account status

![](../.gitbook/assets/image%20%2871%29.png)

### Account Users

Review account's users.

The hosted customer console allows new users to sign up to an account. To allow new users to sign up only via a personal invitation, switch **ON** the option "**Prevent users to signup to this account without invitation**"

![](../.gitbook/assets/image%20%2863%29.png)

### Account Application 

![](../.gitbook/assets/image%20%2817%29.png)

### Account Events 

the account events tab shows an audit log of all the events occurred to an account.

![](../.gitbook/assets/image%20%2819%29.png)



