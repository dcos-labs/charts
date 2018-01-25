# Beer demo ingress controller Helm chart

## Cloudflare Warp

The Cloudflare Warp Ingress Controller makes connections between a Kubernetes service and the Cloudflare edge, exposing an application in your cluster to the internet at a hostname of your choice. A quick description of the details can be found at https://warp.cloudflare.com/quickstart/.

**Note:** Before installing Cloudflare Warp you need to obtain Cloudflare credentials for your domain zone.
The credentials are obtained by logging in to https://www.cloudflare.com/a/warp, selecting the zone where you will be publishing your services, and saving the file to local folder.

To deploy Cloudflare Warp Ingress Controller run:

```bash
helm install --name beer-ingress --namespace beer dlc/cloudflare-warp-ingress --set cert=$(cat cloudflare-warp.pem | base64)
```

Check that pods are running:

```bash
kubectl -n beer get pods
NAME                                                    READY     STATUS    RESTARTS   AGE
beer-ingress-cloudflare-warp-ingress-3061065498-v6mw5   1/1       Running   0          1m
```

## Testing external access

Now you should be able to check beer at https://beer.mydomain.com/
And if you noticed Cloudflare Warp creates `https` connection by default :-)

## Remove

The release can be cleaned up with helm:

```bash
helm delete --purge beer-ingress
```
