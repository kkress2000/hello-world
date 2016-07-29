# hello-world
This project demonstrates two approaches to building a static Hello World web site using cloudformation. 

The first -- Simplistic -- was lifted from AWS documentation. It creates a webserver and load balancer with public interfaces in the default VPC. Protecting the webserver relies on a single set of port restrictions for SSH and HTTP. Without subnets, there are can be no network ACLs. Security protections are defined inline which scales poorly.

The second -- VpcAndSgs -- is more complex. It builds on reusable blocks like a three-layered set of multi-zone subnets -- app, web and database. The security groups already exist and have become reusable building blocks. The downside is that the template assumes that the plumbing is in place. Whether that plumbing is up to code is hidden from view.

The third -- VpcAndSgsCreation -- builds a three-layered, multi-zone VPC from scratch. Make sure the IP address chosen doesn't interfere with your own network and then try it out. The entire structure can be built in minutes and is small enough to serve a single client. With a little tweaking of the address ranges, the VPC can be enlarged ... or it can be scaled out on a per project, per client basis.

##Validation
A simple test with curl reveals the redirect to SSL:
```
$ curl -I http://hwcompletetwo-dev.imt-aws.com/
  HTTP/1.1 302 Found
  Content-Type: text/html; charset=iso-8859-1
  Date: Fri, 29 Jul 2016 01:27:04 GMT
  Location: https://hwcompletetwo-dev.imt-aws.com/
  Server: Apache/2.2.31 (Amazon)
  Connection: keep-alive
```
