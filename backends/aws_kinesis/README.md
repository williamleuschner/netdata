# Using netdata with AWS Kinesis Data Streams

## Prerequisites

To use AWS Kinesis as a backend AWS SDK for C++ should be [installed](https://docs.aws.amazon.com/en_us/sdk-for-cpp/v1/developer-guide/setup.html) first. `libcrypto`, `libssl`, and `libcurl` are also required to compile netdata with Kinesis support enabled. Next, netdata should be re-installed from the source. The installer will detect that the required libraries are now available.

If AWS SDK for C++ is being installed from sources, it is useful to set `-DBUILD_ONLY="kinesis"`. Otherwise, the building process could take a very long time.

## Configuration

To enable data sending to the kinesis backend set the following options in `netdata.conf`:
```
[backend]
    enabled = yes
    type = kinesis
    destination = us-east-1
```
set the `destination` option to an AWS region.

In the netdata configuration directory run `./edit-config aws_kinesis.conf` and set AWS credentials and stream name:
```
# AWS credentials
aws_access_key_id = your_access_key_id
aws_secret_access_key = your_secret_access_key

# destination stream
stream name = your_stream_name
```
Alternatively, AWS credentials can be set for the *netdata* user using AWS SDK for C++ [standard methods](https://docs.aws.amazon.com/sdk-for-cpp/v1/developer-guide/credentials.html).

A partition key for every record is computed automatically by the netdata with the purpose to distribute records across available shards evenly.


[![analytics](https://www.google-analytics.com/collect?v=1&aip=1&t=pageview&_s=1&ds=github&dr=https%3A%2F%2Fgithub.com%2Fnetdata%2Fnetdata&dl=https%3A%2F%2Fmy-netdata.io%2Fgithub%2Fbackends%2Faws_kinesis%2FREADME&_u=MAC~&cid=5792dfd7-8dc4-476b-af31-da2fdb9f93d2&tid=UA-64295674-3)]()
