---
layout: post
title: "4 совета для грамотной работы с CSS"
date: 2015-04-20 03:13:32 +0300
comments: true
categories: ["CSS", "Frontend"]
---
Достаточно взглянуть на [удивительные вещи](http://www.creativebloq.com/web-design/examples-css-912710), которые люди делают с поммощью CSS, чтобы понять - язык меняется. Люди создают [ошеломляющие анимации](http://www.creativebloq.com/css3/animation-with-css3-712437) и [удивительные композиции](http://www.creativebloq.com/css3/css-images-712440).

Будь вы только начинающим, или имеете несколько лет стажа за плечами - ландшафт для разработки CSS разительно поменялся за последние несколько лет. Сейчас есть множество инструментов в вашем распоряжении, которые помогут создать высококачественный и в тоже время короткий CSS. 
<!--more-->
Ниже несколько приемов от [Jonathan Snook](http://www.creativebloq.com/web-design/4-tips-smarter-css-workflow-11514036), которые помогут создать легковесный и быстрый CSS

### 01. Найдите неиспользуемый код

Со временем проэкты меняют внешний вид, а CSS может остаться прежним. Неиспользуемый CSS влияет на производительность, отсылая бесполезный код браузеру и заставляя его работать, чтобы определить какие стили должны быть применены.

[UnCSS](https://github.com/giakki/uncss) берет список всех используемых файлов (ссылок) и проверяет наличие HTML используеющего стиль, после чего выдает CSS файл, содержащий только используемые стили.

UnCSS требует скомпилированого HTML и CSS, а потому может быть не настолько полезен в процессе разработки.

### 02. Определите дублирующийся код

При создании вы работаете с определенными кусочками дизайна. Когда все сделано, вы можете не осознавать, что множество стилей для модального окна, на самом деле очень схожи со стилями для выпадающего списка. 

[csscss](http://zmoazeni.github.io/csscss/) - чекер на избыточность, поможет определить одинаковые свойства используемые вашим CSS, что поможет объединить несколько правил в одно. 

### 03. Определите "плохой" код

Вы определили дублирующийся и не используемый код. Какие еще улучшения можно привнести в наш CSS? [Parker](https://github.com/katiefenn/parker) и [analyze-css](https://github.com/macbre/analyze-css) - два инструмента, которые помогут оценить качество вашего кода.

И _Parker_, и _analyze-css_ могут помочь найти части кода, которые подлежат рефакторингу либо их можно упростить.

### 04. Пишите "хороший" код

Избавление от "плохого" кода - это конечно же хорошо, но почему-бы не писать сразу "хороший" код? Специально для этого есть руководства:
[Руководство по CSS](http://cssguidelin.es/) [Руководство по SASS](http://sass-guidelin.es/). Также рекомендуется к прочтению [SMACSS](http://smacss.com/), где можно почерпнуть идеи, как писать модульный сжатый код для вашего проекта

_Перевод. [4 tips for a smarter CSS workflow](http://www.creativebloq.com/web-design/4-tips-smarter-css-workflow-11514036)_
