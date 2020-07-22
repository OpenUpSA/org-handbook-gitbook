# CDN in front of S3

A CDN in front of S3 can reduce the cost of transfers to the internet from user requests if files are served from the CDN cache at least some of the time.

Cloudfront doesn't have this benefit, as its egress cost is very close to that of S3. To get this cost saving, you have to use a cache outside AWS.

## Bucket name matches hostname

This is the intended way to do this. S3 uses the hostname to identify the bucket that files should be served from.

## Bucket name does not match hostname

If the bucket name does not match the hostname, e.g. because it's an old bucket and you don't want to move all data and integrations to a different bucket name and your CDN doesn't allow sending a custom hostname in the `Host` header, you can use the following setup. This is a bit complex, so consider whether it is the simplest to set up and maintain, or if you're just better off moving to a bucket that matches the domain.

Cloudflare's free tier doesn't allow sending a custom `Host` header, so we need another way to serve the files from the correct bucket. We use Cloudfront for that.

![](https://docs.google.com/drawings/d/e/2PACX-1vSUoINr_UPVQXNf_ohM0gzBNkxmAZZ5nLr42AJaWtn6F4BdvRYPojlqwvBq7gUwzvfFwpZ6P2nuQJTn/pub?w=1327&h=623)

### Use CloudFront to serve the files from S3 instead of S3 directly

1. Start creating a cloudfront distribution
2. Instead of writing a hostname, select the bucket name in the Origin field
3. Leave cache settings to ignoring cookies, headers and query strings
4. Select the cheapest Price Class \(US, Canada, Europe\)
5. Add the intended hostname to the CNAMEs field. 
   1. CloudFlare sends forwards the hostname to the upstream server, and we want the upstream \(cloudfront\) to know that it can serve content for this hostname.
   2. Cloudfront doesn't forward the host header by default, and knows how to server content directly from S3, so this host header won't be a problem for S3.
6. Create a custom certificate using the AWS certificate manager
   1. Copy the ARN from the certificate manager into the custom certificae field as the suggestions don't refresh without reloading the page
7. Save the distribution and copy the Distribution Name e.g. `d14277ixqps6n1.cloudfront.net`

### Point your CDN at cloudfront

Point your CDN at the Distribution Name, NOT the intended hostname.

Point the intended hostname at your CDN.

### Cloudflare

If you are using cloudflare as your CDN and DNS server, you can set it up as follows

1. Create a CNAME for your static files, e.g. static.myapp.com
2. Enter your CloudFront Distribution Name in the content field for the CNAME
3. Leave Proxy Status on Proxied so that CloudFlare's servers cache and serve the content

