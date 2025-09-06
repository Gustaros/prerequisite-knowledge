# Пример архитектуры

Пример архитектуры: **микросервисное приложение для прогноза погоды**, состоящее из фронтенда, сервисов с логикой, и базы данных, работает в Kubernetes<sup>[1]</sup> <sup>[2]</sup>.

## Схема работы приложения

- **Weather-front**: веб-интерфейс, позволяет вводить город и получать прогноз<sup>[1]</sup>.
- **Weather-services**: сервис, принимает запрос от фронтенда, обращается к внешнему API погоды и возвращает результат<sup>[1]</sup>.
- **Weather-db**: база данных, сохраняет историю запросов и результатов<sup>[1]</sup>.
- Каждый компонент — отдельный микросервис, развёрнутый как контейнер.

### Поток запроса

1. Пользователь вводит город на сайте (Weather-front)<sup>[1]</sup>.
2. Weather-front передаёт город Weather-services.
3. Weather-services берёт данные из Weather-db и/или из внешнего погодного API.
4. Ответ возвращается пользователю, результат хранится в базе данных.

## Как помогает Kubernetes

- **Автоматизация развертывания**: для каждого микросервиса описывают объект Deployment, и Kubernetes сам запускает нужное количество экземпляров (подов)<sup>[6]</sup> <sup>[1]</sup>.
- **Горизонтальное масштабирование**: если резко увеличивается число запросов, Kubernetes может автоматически добавить новые копии сервисов под нагрузку<sup>[3]</sup> <sup>[1]</sup>.
- **Самовосстановление**: при сбое контейнера Kubernetes сам перезапустит нужный сервис, пользователь этого не заметит<sup>[6]</sup>.
- **Обновления и откаты**: можно выкатить новую версию микросервиса — Kubernetes обновит поочерёдно поды с минимальными простоями. При ошибке откатится на старую версию<sup>[2]</sup> <sup>[6]</sup>.
- **Мониторинг и балансировка**: прочие инструменты (например, readiness/liveness probes) поддерживают отказоустойчивость и отслеживают работоспособность сервисов<sup>[5]</sup>.
- **Разделение ресурсов**: каждый сервис может работать на разных языках, с разными зависимостями — Kubernetes управляет этим и равномерно распределяет нагрузку между серверами<sup>[6]</sup>.

**Вывод:** Kubernetes превращает ручное управление десятками микросервисов в полностью автоматизированную систему, где приложение устойчиво к сбоям, масштабируется, обновляется и оптимально использует ресурсы<sup>[2]</sup> <sup>[6]</sup> <sup>[1]</sup>.

[1]: https://habr.com/ru/companies/otus/articles/547552/
[2]: https://selectel.ru/blog/what-is-microservice-architecture/
[3]: https://bigdataschool.ru/blog/kafka-and-kubernetes-microservice-architecture-sixfold-case/
[4]: https://servercore.com/ru/blog/articles/how-managed-kubernetes-helps-business-maintain-service-accessibility/
[5]: https://slurm.io/blog/prilozheniya-v-kubernetes-razvertyvanie-slozhnyh-konfiguracij
[6]: https://smartgopro.com/novosti2/kubernetes/
[7]: https://habr.com/ru/companies/otus/articles/562214/
[8]: https://www.reddit.com/r/kubernetes/comments/omno11/example_of_microserviceoriented_application_for/
[9]: https://www.youtube.com/watch?v=pq2swO_zRk8