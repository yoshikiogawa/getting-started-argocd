# ArgoCD

## セットアップ

1. ArgoCDインストール

    ```
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    ```

1. リソースの確認
    ```
    kubectl get pod -n argocd
    NAME                                                READY   STATUS    RESTARTS   AGE
    argocd-application-controller-0                     1/1     Running   0          6m53s
    argocd-applicationset-controller-6b4b7969b8-98qfb   1/1     Running   0          6m53s
    argocd-dex-server-6445d44bd9-7brsd                  1/1     Running   0          6m53s
    argocd-notifications-controller-98464fc99-td8hq     1/1     Running   0          6m53s
    argocd-redis-5dff748d9c-4ng25                       1/1     Running   0          6m53s
    argocd-repo-server-7778dffc44-dztjw                 1/1     Running   0          6m53s
    argocd-server-5f687c8b99-fp6n2                      1/1     Running   0          6m53s
    ```

1. ポートフォワード

        ```
        kubectl -n argocd port-forward service/argocd-server 8080:443
        ```

1. ArgoCDログイン

    ブラウザから `https://localhost:8080`　へアクセス

    - username: `admin`
    - password: `kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath='{.data.password}' | base64 --decode`

## アプリケーションのデプロイ

1. AppProject
    ```
    kubectl apply -f argocd-appproject-test.yaml
    ```
1. Application

    ```
    kubectl apply -f argocd-application-test.yaml
    ```

