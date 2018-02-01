# Webhook slack example

## setup

get `kubeless` client

```
brew install kubeless
```

deploy kubeless on your k8s cluster

```
export RELEASE=v0.3.4
kubectl create ns kubeless
kubectl create -f https://github.com/kubeless/kubeless/releases/download/$RELEASE/kubeless-$RELEASE.yaml
```

## slack webhook

Create SLACK webhook... +Add app

## Launch function

```
$ kubeless function deploy stargazers --runtime ruby2.4 --from-file ./stargazers.rb --handler stargazers.handler --trigger-http --env "WEBHOOK_URL=https://hooks.slack.com/services/T0PSVT.../....."
$ kubeless function describe stargazers
Name:        	stargazers                                                                      
Namespace:   	default                                                                         
Handler:     	stargazers.handler                                                              
Runtime:     	ruby2.4                                                                         
Type:        	HTTP                                                                            
Topic:       	                                                                                
Label:       	{"created-by":"kubeless"}                                                       
Envvar:      	[{"name":"WEBHOOK_URL","value":"https://hooks.slack.com/services/T0PS.../B9...
```

If you want to test it without having a public Ingress, you can use a local ngrok tunnel

```
kubeless route create stargazers --function stargazers
ngrok http -host-header=stargazers.192.168.99.100.nip.io 192.168.99.100:80
```

## Configure GitHub WebHook
