# codefresh

use these commands to get the IP, Cert and Token

IP
export CURRENT_CONTEXT=$(kubectl config current-context) && export CURRENT_CLUSTER=$(kubectl config view -o go-template="{{\$curr_context := \"$CURRENT_CONTEXT\" }}{{range .contexts}}{{if eq .name \$curr_context}}{{.context.cluster}}{{end}}{{end}}") && echo $(kubectl config view -o go-template="{{\$cluster_context := \"$CURRENT_CLUSTER\"}}{{range .clusters}}{{if eq .name \$cluster_context}}{{.cluster.server}}{{end}}{{end}}")

Cert
echo $(kubectl get secret -o go-template='{{index .data "ca.crt" }}' $(kubectl get sa default -o go-template="{{range .secrets}}{{.name}}{{end}}"))

Token
echo $(kubectl get secret -o go-template='{{index .data "token" }}' $(kubectl get sa default -o go-template="{{range .secrets}}{{.name}}{{end}}"))
