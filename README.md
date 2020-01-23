## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/kmayer10/helm-charts/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/kmayer10/helm-charts/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

#######################################################################
  kubectl create serviceaccount --namespace kube-system tiller
  kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
  kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
  cat tiller.yaml
  kubectl apply -f tiller.yaml
  kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
  helm install --name demo mychart-0.1.1.tgz
  kubectl get pods --all-namespaces
  kubectl describe pod tiller-deploy-5b9cc85cf4-82vhx -n kube-system
  kubectl get nodes
  kubectl uncordon ip-172-31-86-85.ec2.internal
  kubectl get nodes
  kubectl describe pod tiller-deploy-5b9cc85cf4-82vhx -n kube-system
  helm install --name demo mychart-0.1.1.tgz
  kubectl delete ns kubernetes-dashboard
  helm install --name demo mychart-0.1.1.tgz
  helm del --purge demo
  helm install --name demo mychart-0.1.1.tgz
#######################################################################################################

#######################
Confnigure-helm.sh
#########################


#!/bin/bash
yum install -y wget
wget https://storage.googleapis.com/kubernetes-helm/helm-v2.12.2-linux-amd64.tar.gz
tar -zxvf helm-v2.12.2-linux-amd64.tar.gz
mv linux-amd64/helm /usr/bin/helm
kubectl -n kube-system create sa tiller
kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller
kubectl create namespace kubeapps
