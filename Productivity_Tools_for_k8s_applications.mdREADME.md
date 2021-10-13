# Productivity Tools for k8s applications
1. Starship
2. kubectx + kubens
3. k9s
4. helm
5. Kubernetes Dashboard
6. kubectl node-shell
7. Custom k8s scripts

## 1. Starship - Cross-Shell Prompt
 - Lives in Github: [https://github.com/starship/starship](https://github.com/starship/starship)
 - Customizable: configure every aspect of your prompt.
 - Universal: works on any shell, on any operating system.
 - Feature rich: support for all your favorite tools.
    See starship config: [https://starship.rs/config/](https://starship.rs/config/)
 - Easy: quick to install – start using it in minutes.

Can be configured using the file `~/.config/starship.toml`
```bash
# Inserts a blank line between shell prompts
add_newline = true

# Replace the "❯" symbol in the prompt with "➜"
[character]                            # The name of the module we are configuring is "character"
success_symbol = "[➜](bold green)"     # The "success_symbol" segment is being set to "➜" with the color "bold green"

# Helm
[helm]
format = "via [⎈ $version](bold white) "

# Python 
[python]
style = "red bold"

# Docker
[docker_context]
format = "via [🐋 $version](blue bold)"

# Display k8s cluster and namespace
[kubernetes]
format = 'on [⛵ $context \($namespace\)](dimmed green) '
disabled = false
```

## 2. kubectx + kubens: Power tools for kubectl
 - Lives in Github: [https://github.com/ahmetb/kubectx](https://github.com/ahmetb/kubectx)
 - kubectx: Utility to manage and switch between k8s cluster contexts
   - Wrapper around the `.kube/config` file
 - kubens: Utility to switch between kubernetes namespaces
   - Basically a substitution of `kubectl config set-context --current --namespace=${NAMESPACE}`

## 3. K9s - Kubernetes CLI To Manage Your Clusters In Style!
 - Lives in Github: [https://github.com/derailed/k9s](https://github.com/derailed/k9s)
 - Tool for operations on pods, especially debugging

## 4. Helm
 - Package manager for k8s resources
 - One Chart is the blueprint for an application
 - A release is an installed instance of the application in the k8s cluster
 - Lifecycle management: Install -> Update <-> Rollback -> Delete
 - Applications within a k8s namespace can be seperated by charts.
 - Templating via `values.yaml`
 - DevOps Services are deployed using helm-charts https://github.developer.allianz.io/CRP/helm-charts

## 5. Kubernetes Dashboard
 - UI for managing k8s resources
 - Basically one triggers `kubectl` commands via this UI. The executed command can be viewed in the k8s dashboard
 - Port forwarding is possible (secured ports as 443 or 8443 can not be forwarded)

## 6. kubectl node-shell
 - Lives in Github: [https://github.com/kvaps/kubectl-node-shell](https://github.com/kvaps/kubectl-node-shell)
 - Start a root shell in the node`s host OS
   - Debug network issues
   - Check storage/cpu consumption
 - Wrapper around the kubernetes cli

## 7. Kubernetes command to list all key-value pairs in a k8s secret
Data section is base64 encoded, therefore retrieving the plain data is not possible without this script
```bash
kubectl get secret $1 -o go-template='{{range $k,$v := .data}}{{printf "%s: " $k}}{{if not $v}}{{$v}}{{else}}{{$v | base64decode}}{{end}}{{"\n"}}{{end}}'
```
