# ☸️ Aprendiendo Kubernetes con Docker

> Repositorio de aprendizaje de **Kubernetes** a partir de aplicaciones empaquetadas con **Docker**.
> Cada módulo parte de una aplicación real, la contenedoriza y la despliega en un clúster paso a paso.

<!-- Badges opcionales: cambia USUARIO/REPO -->
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Licencia](https://img.shields.io/badge/licencia-MIT-green)

---

## 📑 Índice

- [Objetivo](#-objetivo)
- [Requisitos previos](#-requisitos-previos)
- [Estructura del repositorio](#-estructura-del-repositorio)
- [Puesta en marcha](#-puesta-en-marcha)
- [Ruta de aprendizaje](#-ruta-de-aprendizaje)
- [Aplicaciones de ejemplo](#-aplicaciones-de-ejemplo)
- [Comandos útiles](#-comandos-útiles)
- [Solución de problemas](#-solución-de-problemas)
- [Recursos](#-recursos)
- [Notas y progreso](#-notas-y-progreso)
- [Licencia](#-licencia)

---

## 🎯 Objetivo

<!-- Describe con tus palabras qué quieres conseguir con este repositorio -->

- Entender los conceptos básicos de Kubernetes (Pods, Deployments, Services…).
- Pasar de una aplicación en Docker / Docker Compose a manifiestos de Kubernetes.
- Practicar configuración, almacenamiento, red y escalado.
- _Añade aquí tus propios objetivos._

---

## 🧰 Requisitos previos

| Herramienta | Versión probada | Para qué se usa |
|-------------|-----------------|-----------------|
| [Docker](https://docs.docker.com/get-docker/) | `x.y.z` | Construir y ejecutar imágenes |
| [kubectl](https://kubernetes.io/docs/tasks/tools/) | `x.y.z` | Interactuar con el clúster |
| [minikube](https://minikube.sigs.k8s.io/) / [kind](https://kind.sigs.k8s.io/) / [k3d](https://k3d.io/) | `x.y.z` | Clúster local |
| [Helm](https://helm.sh/) _(opcional)_ | `x.y.z` | Gestión de paquetes |

Conocimientos recomendados: terminal básica, Docker (imágenes, contenedores, volúmenes) y YAML.

---

## 📂 Estructura del repositorio

```text
.
├── apps/                    # Código fuente de las aplicaciones de ejemplo
│   └── <nombre-app>/
│       ├── src/
│       ├── Dockerfile
│       └── docker-compose.yml
├── k8s/                     # Manifiestos de Kubernetes
│   └── <nombre-app>/
│       ├── namespace.yaml
│       ├── deployment.yaml
│       ├── service.yaml
│       ├── configmap.yaml
│       ├── secret.example.yaml
│       └── ingress.yaml
├── modulos/                 # Lecciones / ejercicios por tema
│   ├── 01-pods/
│   ├── 02-deployments/
│   └── ...
├── scripts/                 # Scripts de ayuda (crear clúster, limpiar, etc.)
├── docs/                    # Apuntes, diagramas, imágenes
└── README.md
```

<!-- Ajusta el árbol a la estructura real de tu repo -->

---

## 🚀 Puesta en marcha

### 1. Clonar el repositorio

```bash
git clone https://github.com/USUARIO/REPO.git
```

```bash
cd REPO
```

### 2. Crear un clúster local

```bash
minikube start
```

<!-- o: kind create cluster --name aprendizaje -->

### 3. Construir la imagen de una aplicación

```bash
docker build -t <nombre-app>:1.0 ./apps/<nombre-app>
```

Cargar la imagen en el clúster local (si no usas un registro):

```bash
minikube image load <nombre-app>:1.0
```

<!-- kind: kind load docker-image <nombre-app>:1.0 -->

### 4. Desplegar en Kubernetes

```bash
kubectl apply -f k8s/<nombre-app>/
```

### 5. Acceder a la aplicación

```bash
kubectl port-forward svc/<nombre-app> 8080:80
```

Abre <http://localhost:8080>.

### 6. Limpiar

```bash
kubectl delete -f k8s/<nombre-app>/
```

---

## 🗺️ Ruta de aprendizaje

| # | Módulo | Conceptos | Estado |
|---|--------|-----------|--------|
| 01 | Contenedores con Docker | Dockerfile, imágenes, Compose | ⬜ |
| 02 | Primer Pod | Pod, `kubectl run`, logs, exec | ⬜ |
| 03 | Deployments y ReplicaSets | Réplicas, rolling updates, rollback | ⬜ |
| 04 | Services | ClusterIP, NodePort, LoadBalancer | ⬜ |
| 05 | Configuración | ConfigMaps, Secrets, variables de entorno | ⬜ |
| 06 | Almacenamiento | Volumes, PV, PVC, StorageClass | ⬜ |
| 07 | Namespaces y recursos | Requests, limits, ResourceQuota | ⬜ |
| 08 | Salud de la app | Liveness, readiness, startup probes | ⬜ |
| 09 | Ingress | Ingress Controller, reglas, TLS | ⬜ |
| 10 | Escalado | HPA, metrics-server | ⬜ |
| 11 | StatefulSets | Bases de datos, identidad estable | ⬜ |
| 12 | Jobs y CronJobs | Tareas puntuales y programadas | ⬜ |
| 13 | Helm | Charts, values, releases | ⬜ |
| 14 | Observabilidad | Logs, métricas, Prometheus/Grafana | ⬜ |

Leyenda: ⬜ pendiente · 🟨 en curso · ✅ completado

---

## 📦 Aplicaciones de ejemplo

| Aplicación | Tecnología | Descripción | Recursos de K8s usados |
|------------|-----------|-------------|------------------------|
| `<app-1>` | _p. ej. Node.js_ | _API REST sencilla_ | Deployment, Service |
| `<app-2>` | _p. ej. Python + PostgreSQL_ | _App con base de datos_ | StatefulSet, PVC, Secret |
| `<app-3>` | _p. ej. Nginx_ | _Frontend estático_ | Deployment, Ingress |

<!-- Opcional: un diagrama de arquitectura por app en docs/ -->

---

## 🛠️ Comandos útiles

```bash
# Estado general
kubectl get all -n <namespace>

# Detalle de un recurso (eventos incluidos)
kubectl describe pod <pod>

# Logs (seguir en tiempo real)
kubectl logs -f <pod>

# Entrar en un contenedor
kubectl exec -it <pod> -- sh

# Escalar un deployment
kubectl scale deployment <nombre> --replicas=3

# Historial y rollback
kubectl rollout history deployment <nombre>
kubectl rollout undo deployment <nombre>

# Cambiar el namespace por defecto
kubectl config set-context --current --namespace=<namespace>
```

---

## 🩺 Solución de problemas

| Síntoma | Posible causa | Cómo investigar |
|---------|---------------|-----------------|
| `ImagePullBackOff` / `ErrImagePull` | La imagen no existe o no está cargada en el clúster | `kubectl describe pod <pod>` |
| `CrashLoopBackOff` | La app arranca y se cae | `kubectl logs <pod> --previous` |
| `Pending` | Faltan recursos o el PVC no se enlaza | `kubectl describe pod <pod>` y `kubectl get events` |
| El Service no responde | Los `selector` no coinciden con las `labels` del Pod | `kubectl get endpoints <svc>` |

<!-- Añade aquí los errores que te vayas encontrando y cómo los resolviste -->

---

## 📚 Recursos

- [Documentación oficial de Kubernetes](https://kubernetes.io/es/docs/home/)
- [Documentación de Docker](https://docs.docker.com/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/quick-reference/)
- _Cursos, libros, vídeos o artículos que estés siguiendo…_

---

## 📝 Notas y progreso

<!-- Diario de aprendizaje: fechas, dudas, conclusiones -->

- **AAAA-MM-DD** — _Qué aprendí / qué me costó._

---

## 📄 Licencia

Este proyecto está bajo la licencia [MIT](LICENSE). <!-- Cambia si usas otra -->

---

<sub>Hecho con ☕ por [Tu Nombre](https://github.com/USUARIO) mientras aprendía Kubernetes.</sub>
