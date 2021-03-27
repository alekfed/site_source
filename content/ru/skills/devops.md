+++
title = "DevOps"
subtitle = "Общий опыт: 2 года"
tags = ['System']
date = 2020-03-27

# For description meta tag
description = "DevOps-инструменты, с которыми мне довелось поработать."

# Comment next line and the default banner wil be used.
banner = 'img/devops.svg'

+++

Мой опыт в области DevOps сосредоточен вокруг нужд компании, занимающейся разработкой e-commerce платформы. На ранних этапах вся инфраструктура разворачивалась через [Docker Compose](https://docs.docker.com/compose/), но впоследствии появилась необходимость перевести всё на [Kubernetes](https://kubernetes.io/).

# Kubernetes

Есть опыт разворачивания кластера через [Kubespray](https://kubespray.io/) и [K3s](https://k3s.io/).

Увы, с появлением кластера возникает куча проблем, о которых даже и не задумываешься, пока его нет. В частности, при наличии кластера локальная разработка приложений идёт в отрыве от фактической ситуации в кластере. Я пробовал организовать локальную разработку на основе локальных миникластеров с утилитами вроде [Tilt](https://tilt.dev/), но, в итоге, по ряду причин вернулся к Compose для локальных сред.

С другой стороны, [Helm](https://helm.sh/) позволяет отойти от голых образов приложений и оперировать всем деплоем приложения как единой сущностью, что упрощает контроль этого приложения в облаке. Для решения вопроса воспроизводимости конфигурации кластера на уровне приложений я пробовал варианты с [Helmfile](https://github.com/roboll/helmfile) и [провайдером Helm к Terraform](https://registry.terraform.io/providers/hashicorp/helm/latest/docs), и остановился на последнем.

# CI/CD

В настройке CI мой опыт ограничен [GitLab](https://docs.gitlab.com/ee/ci/) и [Drone](https://www.drone.io/). Последним я заинтересовался, когда обнаружил, что GitLab'овские воркеры могут без проблем выжирать по 10Гб ОЗУ на **один** воркер и надо было что-то с этим делать. Но в какой-то момент появилась возможность перенести GitLab на отдельный сервер с кучей ОЗУ, так что вариант с Drone утратил актуальность.

# FaaS

За последние пару лет AWS Lambda-подобные сервисы набрали популярность, и даже появилась возможность развернуть FaaS в собственном кластере. У меня есть опыт разворачивания и написания функций для [OpenFaaS](https://www.openfaas.com/).

# Nix

*Эта тема также затронута на странице по моим навыкам в операционных системах*

Другая интересная идея, которой я занимаюсь последнее время — декларативно-конфигурируемые дистрибутивы Linux для использования их в качестве базовых систем или даже альтернативы тяжеловесным кластерам. К таковым, на сегодняшний день, серьёзно можно отнести только [NixOS](https://nixos.org/) (нет, не [Guix](https://guix.gnu.org/)). Я пытаюсь поддерживать конфигурацию [своей NixOS](https://git.sr.ht/~alekfed/nix-config/tree), но было бы интересно попробовать эту систему для более масштабных задач.

___
## Иллюстрация

- Заглавная надпись: логотип [AWS](https://aws.amazon.com/). Я иногда ориентируюсь на их решения в области веб-сервисов, когда прорабатываю вопросы инфраструктуры. Жаль, что порой их цены оставляют желать лучшего.

- Визуализация инфраструктуры в виде "парящих коробок": вероятно, я решил сделать что-то подобное просматривая страницы [ELK](https://www.elastic.co/what-is/elk-stack) и [Vault](https://www.hashicorp.com/products/vault). Логотипы возле плиток говорят сами за себя: HCL-скриптами обеспечиваем конфигурации машин ([Terraform](https://www.terraform.io/)), плейбуками — конфигурации систем ([Ansible](https://www.ansible.com/)), ресурсами — кластеров ([Kubernetes](https://kubernetes.io/)), чартами — приложений ([Helm](https://helm.sh/)). Справедливости ради стоит отметить, что порой границы между слоями не такие уж и строгие. К примеру, как упоминалось выше, Terraform'овские HCL-скрипты вполне могут описывать и конфигурацию Kubernetes-кластеров на уровне Helm-чартов.

- Логотипы на слое Helm — чарты упрощают жизнь: можно относительно безболезненно развернуть в кластере и маршрутизатор с автоматическим TLS ([Traefik](https://traefik.io/traefik/)), и хранилище секретов с авторотацией ключей ([Vault](https://www.hashicorp.com/products/vault)), и фичастую среду для контроля исходного кода ([GitLab](https://gitlab.com/)), и даже навертеть на всё метрики ~~без регистрации и смс~~ ([Prometheus](https://prometheus.io/)).