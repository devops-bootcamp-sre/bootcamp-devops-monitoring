#### Estructura de Repositorios

##### Repositorio: `bootcamp-devops-monitoring`
Este repositorio contiene todos los manifiestos necesarios para crear los Deployments de cada herramienta de monitoreo.

Estructura de directorios:
- `grafana/`
- `kube-state-metrics/`
- `kubernetes-node-exporter/`
- `prometheus/`

##### Repositorio: `bootcamp-devops-gitops`
Este repositorio contiene el archivo de tipo `application` de ArgoCD, que especifica el repositorio `bootcamp-devops-monitoring` para crear los Deployments.

Ruta del archivo:
- `pipelines/bootstrap/bootstrap-monitoring.yaml`

### Pasos para Desplegar el Sistema de Monitoreo

#### 1. Crear la Aplicación de ArgoCD

Utiliza el archivo `pipelines/bootstrap/bootstrap-monitoring.yaml` para crear la aplicación en ArgoCD. Este archivo especifica el repositorio `bootcamp-devops-monitoring` y la ruta para los manifiestos de los Deployments.

**Comando:**
```bash
kubectl apply -n argocd -f pipelines/bootstrap/bootstrap-monitoring.yaml
```

#### 2. Verificar la Creación de la Aplicación en ArgoCD

Una vez que ejecutes el comando anterior, ArgoCD se encargará de crear todos los recursos especificados en `bootcamp-devops-monitoring`. Puedes verificar el estado de la aplicación desde la interfaz web de ArgoCD.

1. Accede a la interfaz web de ArgoCD.
2. Busca la aplicación creada (el nombre dependerá de la configuración en el archivo `bootstrap-monitoring.yaml`).
3. Verifica que todos los recursos se hayan creado correctamente y que no haya errores.

#### 3. Confirmar el Despliegue de Herramientas de Monitoreo

Verifica que cada componente de monitoreo esté desplegado y funcionando correctamente:

- **Grafana**: Deberías poder acceder a la interfaz web de Grafana y ver los dashboards disponibles.
- **kube-state-metrics**: Verifica que el Deployment y el Service estén corriendo.
- **kubernetes-node-exporter**: Confirma que el DaemonSet esté corriendo en todos los nodos.
- **Prometheus**: Asegúrate de que el Deployment y el Service estén corriendo y que Prometheus esté scrapeando las métricas de los otros componentes.
