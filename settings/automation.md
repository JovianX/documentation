# Automation

Automation allows creating automation rules, that trigger actions based on JovianX events. Once a rule is triggered it calls an action webhook, that can send information from JovianX to external cloud services. **Automation** effectively allows integration with external services such as [HubSpot](https://hubspot.com), [Slack](https://slack.com), [Jira](https://www.atlassian.com/software/jira), [Freshdesk](https://freshdesk.com/), [Pager Duty](https://pagerduty.com/) and others. 

![](../.gitbook/assets/image%20%2851%29.png)

### Events‌

JovianX allows configuring automation rules for the following events:

* Customer account created
* Customer account deleted
* Customer account trial is over
* Customer account user created
* Customer account user logged in
* Application helm parameters changed
* Application launch settings changed
* Application upgraded
* Application error
* Email notification sent

### Actions

JovianX supports the following action Types:

{% tabs %}
{% tab title="Webhook" %}
### Webhook

JovianX calls a webhook when an automation rule is triggered. ‌To configure a Webhook set the following settings:

#### URL 

The URL of the Webhook Must be a valid web address URI.

#### ‌Method

You can define the URL method for JovianX to trigger, following methods are supported:

* GET
* POST
* PUT
* PATCH

#### **Headers**

Custom headers are supported, you can  define a custom `key: value` pairs of headers. Additionally, you can use **variables** as header `values`:

![](../.gitbook/assets/image%20%2825%29.png)

**Content:** 

The content section holds the Webhook request content data, you can define the content type and configure the data to send. 

**Content Type**

* JSON
* MULTIPART/FORM-DATA
* X-WWW-FORM-URLENCODED

**JSON** content-type allows defining the JSON content data:

![](../.gitbook/assets/image%20%286%29.png)

**MULTIPART/FORM-DATA** and **X-WWW-FORM-URLENCODED** allow setting the `key:value` data:

![](../.gitbook/assets/image%20%2873%29.png)
{% endtab %}
{% endtabs %}

### Available Variables

Events expose a set of **variables** that can be used as event data or headers when triggering an action:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Event</th>
      <th style="text-align:left">Supported Variables</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p><b>Customer account created</b>
        </p>
        <p>Event triggered on successful customer account creation.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Customer account deleted</b>
        </p>
        <p>Event triggered on deletion of customer account.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Customer account trial is over</b>
        </p>
        <p>Event triggered when customer account trial period is over.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Customer account user created</b>
        </p>
        <p>Event triggered on creation of new account user</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{user_email}}</b>: User email address</p>
        <p><b>{{user_name}}</b>: User full name</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Customer account user logged in</b>
        </p>
        <p>Event triggered when account user logs into the customer console.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{user_email}}</b>: User email address</p>
        <p><b>{{user_name}}</b>: User full name</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Application helm parameters changed</b>
        </p>
        <p>Event triggered on update of application &apos; &apos;components helm
          parameters.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{parameters}}</b>: Application components helm parameters after successful
          update</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Application launch settings changed</b>
        </p>
        <p>Event triggered when account settings are changed.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{parameters}}</b>: Application components helm parameters after successful
          update</p>
        <p><b>{{application_settings}}</b>: New application settings chosen by user.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Application upgraded</b>
        </p>
        <p>Event triggered after successful application blueprint &apos; &apos;version
          change.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{parameters}}</b>: Application components helm parameters after successful
          upgrade.</p>
        <p><b>{{old_blueprint_version}}</b>: Application blueprint version before
          upgrade</p>
        <p><b>{{new_blueprint_version}}</b>: Application blueprint version after
          upgrade</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Application error</b>
        </p>
        <p>Event triggered when application state changes to &quot;error&quot;.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{previous_state}}</b>: Application state before it was changed to
          &quot;error&quot;</p>
        <p><b>{{parameters}}</b>: Application components helm parameters</p>
        <p><b>{{application_settings}}</b>: Application settings chosen by user</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>Email notification sent</b>
        </p>
        <p>Event triggered after an email notification is sent.</p>
      </td>
      <td style="text-align:left">
        <p><b>{{account_id}}</b>: Account identifier</p>
        <p><b>{{account_display_name}}</b>: Account company name provided during
          registration</p>
        <p><b>{{receiver}}</b>: To whom notification was sent</p>
        <p><b>{{subject}}</b>: Subject of the email notification</p>
        <p><b>{{message}}</b>: Body of the email notification</p>
      </td>
    </tr>
  </tbody>
</table>

### Creating a new automation Rule

To create a new automation rule :

1. Navigate to `Settings` &gt; `Automation` on the side-menu.
2. Click on Create rule button on the upper left side

![](../.gitbook/assets/jovianx-saas-platform-1-.gif)





#### Example JovianX &gt; Slack integration:

![](../.gitbook/assets/image%20%2848%29.png)



