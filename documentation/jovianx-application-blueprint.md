# Blueprints

### Introduction

An application blueprint is a packaged tarball file \(`*.tar.gz`\) that contains the application manifest YAML file \(`jovianx.yaml`\) and the Helm Charts directories that are referenced by the application manifest. The application manifest defines the components used by the application. The components can be Helm Charts or other cloud-managed services. JovianX uses the Application Blueprint to create resources and set up services when a new account signs up.

### Blueprint Structure

The application blueprint contains the following:

1. **Application Manifest** - The application manifest  is a YAML file named `jovianx.yaml`. The manifest defines the components that are created for a new SaaS account. For example Kubernetes Helm Charts, DynamoDB, CloudDNS or other cloud managed services.
2. **Helm Charts -** The blueprint can also include the Helm Charts that are used for creation of application services.

### Application Manifest\(`jovianx.yaml`\)

The application manifest is a YAML file that describes the application. JovianX uses the manifest to create the needed resources and services when a new account signs-up.

A basic template of an application manifest looks as following:

{% code title="jovianx.yaml" %}
```yaml
# v1 - JovainX API Compatability
jovianx_api_version: v1

# string - Name of this SaaS application
application_name: '<APP-NAME>'

# semantic versioning - version of this JovianX blueprint 
version: <SEM-VERSION>

# string - Name of a component to be used a main application entry point 
main_endpoint_component: '<COMPONENT-NAME>'

# Components section defines all application components and their helm chart implementations
components:
  - name: '<COMPONENT-NAME>'
    version: <COMPONENT-SEMVER>
    provider: helm_chart
    helm_chart_name: <PATH/TO/HELM/CHART>
    helm_set:
      # List of key-value pairs to pass to helm on account creation
      - key: '<SET-KEY>'
        value: '<SET-VALUE>'
    endpoints:
      - name: '<ENTRYPOPINT-NAME>'
        type: entry_point
        service_name: '<KUBERNETS-SERVICE-NAME>'
        port: <KUBERNETES-SERVICE-PORT>
        path: '<KUBERNETES-SERVICE-PATH>'

# Settings Descripts define user inputs and 
settings_descriptors:
  # list of descriptos
  - name: <DESCRIPTOR-NAME>
    display: '<A QUESTION TO ASK THE USER ON SIGN-UP>'
    input_type: string
    default: '<DEFAULT ANSWER>'
    components:
      - name: '<COMPONENT-NAME>' # Provide value to this componet 
        helm_set:
          - key: '<SET-KEY>'
```
{% endcode %}

### Creating Application Blueprint

To create an application blueprint archive the application manifest and helm charts into a blueprint tar.gz

```text
$ tar -cf <BLUEPRINT-NAME> jovianx.yaml <HELM-CHART> ...
```

{% hint style="info" %}
Note: The Helm Charts should be open, untar direcotry.
{% endhint %}

Example: the following directory has an application manifest `jovianx.yaml` and a Chart `my-helm-chart`

```bash
├── my-helm-chart
│   ├── charts
│   ├── templates
│   ├── Chart.yaml
│   └── values.yaml
└── jovianx.yaml
```

To create an application blueprint for the directory use the following command:

```text
$ tar -cf blueprint-1.0.0.tar.gz jovianx.yaml my-helm-chart
```

### Upload Application Blueprint

#### Upload Blueprint via Web UI

To upload your application blueprint to JovianX via the web console:

1. Navigate to Blueprints page
2. Click on `Upload a new Blueprint` bar
3. Click on `Choose blueprint tar.gz` file
4. Click on `Upload` to upload your blueprint

![](../.gitbook/assets/screenshot-20190825125210-1252x389.png)

Once the blueprint is upload you will be able to find it in the blueprints list, and view the application manifest.

#### Upload Blueprint via CURL\(CI\)

To upload your application blueprint to JovianX via an automated CI process or from command line, you will need to find your `API Access Key` and `API Secret`. You can find both in `Upload a new Blueprint` bar under `Blueprints` navigation bar.

```text
curl -u '<ACCOUNT-API-ACCESS-KEY>:<API-SECRET>' -F 'file=@<PATH/TO/BLUEPRINT/FILE.TAR.GZ>' 'https://<ACCOUNT-API-PATH>/api/v1/upload_blueprint?make_default=true'
```

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
      <td style="text-align:left"><a href="jovianx-application-blueprint.md#components"><code>components</code></a>
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
      <td style="text-align:left"><code>status_check:</code>
        <br /> <code>failure_threshold:</code>
      </td>
      <td style="text-align:left">
        <p><b>Description</b>: How many status error detection are accepted before
          changing the app status to error.</p>
        <p><b>Parent</b>: Root Type: collection</p>
        <p><b>Default</b>: 1</p>
        <p>Optional</p>
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
        <p><b>Required for</b>  <code>helm_chart</code> provider</p>
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
        <p><b>Optional for</b>  <code>helm_chart</code> provider</p>
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
        <p> <code>- key: image</code>
        </p>
        <p> <code>value: registry.hub.docker.com/my-company/image</code>
        </p>
        <p><b>Optional for</b>  <code>helm_chart</code> provider</p>
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

```text
{{ account://application_version}}
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

