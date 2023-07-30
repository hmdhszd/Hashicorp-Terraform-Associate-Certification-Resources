

## Make use of the output of one resource and use it in another resource


first, we should check the documents of each provider:

  time_static    :    https://registry.terraform.io/providers/hashicorp/time/latest/docs/resources/static


__________________________________________________________________________________________



then check the "Read-Only" part to see what output of this provider can be used in another provider:

for example for the "time_static" provider:


Read-Only:


day: (Number) Number day of timestamp.

hour: (Number) Number hour of timestamp.

id: (String) RFC3339 format of the offset timestamp, e.g. 2020-02-12T06:36:13Z.

minute: (Number) Number minute of timestamp.

month: (Number) Number month of timestamp.

second: (Number) Number second of timestamp.

unix: (Number) Number of seconds since epoch time, e.g. 1581489373.

year: (Number) Number year of timestamp.


__________________________________________________________________________________________


${time_static.time_update.id}

```bash
 resource "time_static" "time_update" {
}

resource "local_file" "time" {
  filename = "/root/time.txt"
  content = "Time stamp of this file is ${time_static.time_update.id}"

 }
```



__________________________________________________________________________________________



Make use of the "terraform show" command and identify the attribute values.


```bash
iac-server $ terraform show
# local_file.time:
resource "local_file" "time" {
    content              = "Time stamp of this file is 2023-07-30T16:19:52Z"
    content_base64sha256 = "sB2Vh/rV1H53e9HzVCBza4Il4HmxwjDUBTy0nv3yjak="
    content_base64sha512 = "njKdqi9G5zEqzHBa9eQNncz3H1cjAnOkMGl/0J1BXmNlBKAdZteZ8lQN6xuhkxWna1kob7UlH2bpDGM1E59DzA=="
    content_md5          = "36986cb098b8b53e39ba1ae63d35f95a"
    content_sha1         = "46fc4361c548c71332795f79a82ace9ad8cbaa74"
    content_sha256       = "b01d9587fad5d47e777bd1f35420736b8225e079b1c230d4053cb49efdf28da9"
    content_sha512       = "9e329daa2f46e7312acc705af5e40d9dccf71f57230273a430697fd09d415e636504a01d66d799f2540deb1ba19315a76b59286fb5251f66e90c6335139f43cc"
    directory_permission = "0777"
    file_permission      = "0777"
    filename             = "/root/time.txt"
    id                   = "46fc4361c548c71332795f79a82ace9ad8cbaa74"
}

# time_static.time_update:
resource "time_static" "time_update" {
    day     = 30
    hour    = 16
    id      = "2023-07-30T16:19:52Z"
    minute  = 19
    month   = 7
    rfc3339 = "2023-07-30T16:19:52Z"
    second  = 52
    unix    = 1690733992
    year    = 2023
}
```



__________________________________________________________________________________________



## These dependencies come in two flavours: 

#### Implicit – where a resource may reference another resource/data source.

#### Explicit – where an engineer explicitly calls out a dependency between two resources/data sources.

for explicit dependency, we should use "depends_on" : 


```bash
resource "local_file" "whale" {
  filename   = "/root/whale"
  content    = "whale"
  depends_on = [
      local_file.krill
      ]
}
resource "local_file" "krill" {
  filename = "/root/krill"
  content  = "krill"
}
```



__________________________________________________________________________________________
