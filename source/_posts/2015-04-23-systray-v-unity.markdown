---
layout: post
title: "systray в Unity"
date: 2015-04-23 02:35:08 +0300
comments: true
categories: ['Unity', 'Ubuntu']
---
Из Unity окончательно убрали значки в трее с последним обновлением. Долгое время для борьбы с этим помогал такой вариант:
```
sudo apt-add-repository ppa:gurqn/systray-trusty
sudo apt-get update
sudo apt-get upgrade

```
<!--more-->
К сожалению, этот способ больше не работает теперь. Для тех кому все же необходимы значки в трее (некоторые программы все же появляются там) поможет решение `Indicator Systemtray Unity`. Установка проста: 
```
sudo apt-add-repository ppa:fixnix/indicator-systemtray-unity
sudo apt-get update
sudo apt-get install indicator-systemtray-unity

```

[Исходник на GitHub](https://github.com/GGleb/indicator-systemtray-unity)

[Обсуждение на Ubuntu форуме](http://forum.ubuntu.ru/index.php?topic=258603.0)

Если не нравится нажимать на индикатор для доступа к иконкам - жмем на индикаторе среднюю кнопку мыши. Подкорректировать положение док-окна можно через `dconf-editor`, раздел `gsettings:/net/launchpad/indicator/systemtray` или прокруткой среднего колесика мыши на индикаторе