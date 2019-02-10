# AWS Secure S3 to CDN Cloudformation

This template assumes you are creating a subdomain and a deligated DNS zone.
you provide the name for the new deligated zone by providing a name and a parent zone. In return you get:
- A new s3 bucket setup as a wesite, but secured.
- A new Cloudfront Distribution with Origin Identity, and HTTP-to-HTTPS redirect.
- Bucket policy on s3 bucket to allow only this distribution access to the bucket
- A certificate will be generated in ACM and a request sent to the parent domain's admin email. Both *.subdomain.domain and subdomain.domain
- A new Route 53 Zone created for the subdomain
- RecordSet for the Cloudfront set to cdn.subdomain.parent_domain
- Apex RecordSet Group for subdomain.parent_domain
-TTL defaults to 60seconds on the Cloudfront Distribution in behaviors. Change that higher for better performance, if the content is not expected to change often.
Things to complete after, manually,
- lookup the NS records for the newly created Route53 Zone
- in the parent DNS zone, create a NS record pointing subdomain.parent_domain to the 4 NS records provided
- add your static content to the s3 bucket


Example:
Parent domain is example.com
new domain is project
this creates a website that is accessable via cdn.project.example.com and project.example.com
the certificate will need to be verified via email from the admin of example.com


