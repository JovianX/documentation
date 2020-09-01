# Blueprints

## Application Manifest \(jovianx.yaml\) Reference

## Application Manifest Root

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>jovianx_api_version</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Version of the JovianX Manifest API.</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: v1</p>
        <p><b>Required</b>
        </p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>application_name</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Name of the SaaS Application.</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: string</p>
        <p><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>version</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Version of the JovianX blueprint.</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: semantic version</p>
        <p><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>main_endpoint_component</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Main application end-point.</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: string</p>
        <p><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="manifest-reference.md#components"><code>components</code></a>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: components section is a list of all components(Helm
          Charts or Cloud Managed Services) used as part of the application, and
          their settings.</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: list
          <br /><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>application_launch_timeout</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Application timeout configuration</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: collection</p>
        <p><b>Optional</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>agents</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: The list of agents</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: list</p>
        <p><b>Optional</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>settings_descriptors</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: A list of settings descriptors</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: list</p>
        <p><b>Optional</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>hooks</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: List of hooks</p>
        <p><b>Parent</b>: Root
          <br /><b>Type</b>: list</p>
        <p><b>Optional</b>
        </p>
      </td>
    </tr>
  </tbody>
</table>

## Components

Components section is a list of all components used as part of the application, and their settings. Components are Helm Charts or Cloud Managed Services.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>name</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Name of the component</p>
        <p><b>Parent</b>: components
          <br /><b>Type</b>: string</p>
        <p><b>Example</b>: <code>name: &apos;my-component&apos;</code>
        </p>
        <p><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>version</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Version of the component</p>
        <p><b>Parent</b>: components
          <br /><b>Type</b>: semantic_version</p>
        <p><b>Example</b>: <code>version: 14.5.2</code>
        </p>
        <p><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>provider</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Provider that implements the component</p>
        <p><b>Parent</b>: components
          <br /><b>Type</b>: Select
          <br /><b>Options</b>:</p>
        <ul>
          <li>helm_chart</li>
          <li>[Additional providers available in private alpha]</li>
        </ul>
        <p><b>Example</b>: <code>provider: helm_chart</code>
        </p>
        <p><b>Required</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>helm_chart_name</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Path to unarchived helm chart within the blueprint</p>
        <p><b>Parent</b>: components
          <br /><b>Type</b>: string</p>
        <p><b>Example</b>: <code>helm_chart_name: /my-helm-chart/</code>
        </p>
        <p><b>Required for </b><code>helm_chart</code> provider</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>helm_values_file</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: Path to values.yaml file for the component</p>
        <p><b>Parent</b>: components
          <br /><b>Type</b>: string</p>
        <p><b>Example</b>: <code>helm_values_file: /my-helm-chart/my-values.yaml</code>
        </p>
        <p><b>Optional for </b><code>helm_chart</code> provider</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>helm_set</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: List of helm set key and value pairs</p>
        <p><b>Parent</b>: components
          <br /><b>Type</b>: list</p>
        <p><b>Example</b>:</p>
        <p><code>helm_set:</code>
        </p>
        <p><code>    - key: image</code>
        </p>
        <p><code>      value: registry.hub.docker.com/my-company/image</code>
        </p>
        <p><b>Optional for </b><code>helm_chart</code> provider</p>
      </td>
    </tr>
  </tbody>
</table>

## Settings Descriptors

| Key | Description |
| :--- | :--- |
| `name` | **Type**: string |
| `display` | **Type**: string |
| `input_type` | **value**: string \| number \| radio \| select |
| `default` | **Type**: string |
| `description_title` | **Type**: string |
| `select_options` | **Type**: list |

## Hooks

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>pre_install</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: List hooks that are executed before app install</p>
        <p><b>Parent</b>: <code>hooks</code>
          <br /><b>Type</b>: list</p>
        <p><b>Optional</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>post_install</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: List of hooks that are executed after app install</p>
        <p><b>Parent</b>: <code>hooks</code>
          <br /><b>Type</b>: list</p>
        <p><b>Optional</b>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### Hook

| Key | Description |
| :--- | :--- |
| name |  |
| on\_failure |  |
| timeout |  |
| provider |  |
| image |  |
| command |  |
| args |  |
| env |  |

## Variables 

### Account

```text
{{ account://vendor_company }}
```

```text
{{ account://end_company }}
```

```text
{{ account://account_api_key }}
```

```text
{{ account://admin_email }}
```

```text
{{ account://admin_password }}
```

```text
{{ account://api_host }}
```

{% code title="example" %}
```text
components:
  - name: node-component
    version: 1.0.0
    provider: helm_chart # helm_chart | docker
    helm_chart_name: node-chart
    helm_values_file: values-jovianx.yaml
    helm_set:
      - key: repository
        value: https://gitlab.com/jovianx-saas-platform/hello-world-app.git
      - key: replicas
        value: 1
      - key: vendor_company
        value: '{{ account://vendor_company }}'
      - key: end_company
        value: '{{ account://end_company }}'
      - key: account_api_key
        value: '{{ account://account_api_key }}'
      - key: admin_email
        value: '{{ account://admin_email }}'
      - key: admin_password
        value: '{{ account://admin_password }}'
      - key: api_host
        value: '{{ account://api_host }}'
```
{% endcode %}

### Application



