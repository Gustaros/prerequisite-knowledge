# Control Plane

Control Plane (управляющий слой) Kubernetes — это набор сервисов и компонентов, которые управляют всем кластером. Он обычно располагается на одном или нескольких специальных узлах, называемых мастер-узлами (control plane nodes). Эти узлы могут быть отдельными физическими или виртуальными серверами, выделенными только для управления кластером.<sup>[1]</sup> <sup>[2]</sup> <sup>[4]</sup>

## Основные компоненты Control Plane

![alt text](control_plane.png)

- **API Server** — точка входа для всех запросов к кластеру, через нее происходит взаимодействие с Kubernetes (например, через kubectl).<sup>[7]</sup> <sup>[1]</sup>
- **Scheduler** — распределяет поды по рабочим узлам на основе ресурсов и правил.<sup>[2]</sup> <sup>[4]</sup>
- **Controller Manager** — следит за состоянием кластера и обеспечивает нужное число подов, обновления, масштабирование и т.д.. <sup>[4]</sup> <sup>[2]</sup>
- **etcd** — распределённое key-value хранилище, где хранится текущая конфигурация и состояние кластера.<sup>[2]</sup> <sup>[4]</sup>

## Где физически находится Control Plane

- В типичном кластере Kubernetes Control Plane развёрнут на одном или нескольких узлах, которые не запускают рабочие нагрузки (поды приложений). Они отвечают исключительно за управление и координацию кластера.<sup>[1]</sup> <sup>[4]</sup>
- Для обеспечения отказоустойчивости Control Plane обычно развёртывают на нескольких узлах, чтобы при сбое одного узла управление переходило к другому.<sup>[3]</sup> <sup>[6]</sup>

## Пример реальной системы Kubernetes с Control Plane

| Компоненты          | Описание                                                   | Расположение                             |
|---------------------|------------------------------------------------------------|----------------------------------------|
| Control Plane Nodes  | Узлы с API Server, Scheduler, Controller Manager, etcd     | Выделенные серверы (физические или ВМ) |
| Worker Nodes (Рабочие узлы) | Узлы, на которых запускаются поды с контейнерами приложений | Физические или виртуальные серверы      |
| Поды (Pods)         | Минимальная единица запуска — один или несколько контейнеров | Запускаются на рабочих узлах            |
| Services            | Абстракция для связи подов, обеспечивающая стабильный IP   | Работают поверх рабочих узлов           |

Пример создания кластера с несколькими Control Plane нодами:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: control-plane
- role: worker
```

Здесь два узла отвечают за Control Plane, обеспечивая высокую доступность, а один — за запуск приложений.

**Итог:** Control Plane — это центральная управляющая часть Kubernetes, обычно развёрнутая на выделенных узлах или серверах, которая координирует работу всего кластера, в то время как сами приложения запускаются на рабочих узлах, распределённых по инфраструктуре.<sup>[3]</sup> <sup>[4]</sup> <sup>[1]</sup> <sup>[2]</sup>

[1]: https://habr.com/ru/companies/flant/articles/583660/
[2]: https://learning.infoteam.msk.ru/Rebrain/K8s/Kubernetes%20v2/KUB%2007%20Kubernetes%20Control%20Plane.pdf
[3]: https://habr.com/ru/companies/first/articles/844002/
[4]: https://ininsys.ru/stati/arhitektura-kubernetes-control-plane-i-worker-nodes/
[5]: https://deckhouse.ru/products/kubernetes-platform/documentation/v1/modules/control-plane-manager/faq.html
[6]: https://androsov-it.ru/%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%B0-kubernetes-1-27-1-%D0%B8%D0%B7-%D1%82%D1%80%D0%B5%D1%85-control-plane-%D1%81-%D0%BF%D0%BE%D0%BC%D0%BE/
[7]: https://kubernetes.io/ru/docs/concepts/overview/components/
[8]: https://labex.io/ru/tutorials/kubernetes-explore-the-kubernetes-cluster-434519
[9]: https://devandops.kz/index.php/lesson/ustanovka-kubernetes/