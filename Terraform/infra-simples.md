

![image](https://user-images.githubusercontent.com/59710101/224498226-f21123b6-74fd-485e-9569-344808cea64e.png)

Cloud shell já possui terraform instalado


## Creating netwwork
```sh
# Create the mynetwork network
resource "google_compute_network" "mynetwork" {
name = "mynetwork"
# RESOURCE properties go here
auto_create_subnetworks = "true"
}

```
