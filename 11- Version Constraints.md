
# Terraform block

you can use a specific version of the terraform provider: (default = latest version)

we use "terraform" block to configure settings related to terraform itself.

inside this block, we use `required_providers` to specify the version of the provider.



__________________________________________________________________________________________




main.tf

```bash
terraform {
  required_providers {
    google = {
      source  = "hashicorp/google"
      version = "> 3.45.0, !=3.46.0, < 3.48.0"
    }
  }
}

resource "google_compute_instance" "special" {
  name         = "aone"
  machine_type = "e2-micro"
  zone         = "us-west1-c"

}
```







__________________________________________________________________________________________
