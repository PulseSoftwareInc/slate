# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint"
  -H "Authorization: Token token=fake_token"
```

> Make sure to replace `fake_token` with your API key.

Data on Reflektive's platform can be retrieved by authenticating with a company's secret API key.

The company's API key can be used to retrieve data on behalf of the entire company. To obtain an API key, please reach out to [support@reflektive.com](mailto:support@reflektive.com)

Authentication to the API is performed via token authentication using HTTP headers. For example, the following header can be used to authenticate:

`Authorization: Token token=fake_token`

<aside class="notice">
You must replace <code>fake_token</code> with your personal API key.
</aside>
