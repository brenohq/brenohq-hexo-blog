---
title: Contribuindo com projetos BOINC no seu Arch Linux
date: 2016-09-09 11:19:27
tags:
- OpenSource
- BOINC
- Tutorial

disqusIdentifier: fdsF34ff34
keywords:
- Contribuindo
- projetos
- BOINC
- Arch
- Linux
- Manjaro
- computação
- distribuída
- open
- source
- processamento
- ocioso
- voluntária
- brenohq
- Breno Henrique
- brenohq.com
- www.brenohq.com  
clearReading: false
thumbnailImage: https://lh5.ggpht.com/WNnBsOZtGqaFxNpcVm0jXz75D3uoXoi9muwPcqG20MjBjdETElwam6FBn1kFdLVZDw=w300
thumbnailImagePosition: right
autoThumbnailImage: yes
metaAlignment: center
coverCaption: "Hora de usar essa carroça pra alguma coisa útil, né?"
coverMeta: out
coverSize: partial
coverImage:
gallery:
comments: true

---

O [BOINC](http://boinc.berkeley.edu/) (Berkeley Open Infrastucture For Network Computing) é uma modelo de infra-instrutura de software, que utiliza os conceitos de computação distribuída. A ideia é substituir a compra e manutenção de gigantescos clusters, pelo poder computacional, disponibilizado por você, de forma voluntária. Hoje vou ensinar como contribuir com esses projetos, usando o seu computador. Bora?

<!-- more -->

-----------------

## Instalando o BOINC Manager

Para instalar o cliente BOINC, basta o seguinte comando:

``` bash
$ sudo pacman -S boinc
```

Com isso, você já tem o boinc instalado, porém é necessário fazer algumas alterações para que ele funcione corretamente:

``` bash
$ cd ~/
$ ln -s /var/lib/boinc/gui_rpc_auth.cfg gui_rpc_auth.cfg
$ sudo chmod 640 gui_rpc_auth.cfg
```

Agora, é so iniciar a aplicação com o comando:

``` bash
$ sudo boincmgr
```

{% image fancybox center boinc_manager.png 300px "Essa tela deverá aparecer." %}

-----------------

## Contribuindo pela primeira vez

Logo após a sincronização, deve aparecer um botão {% hl_text danger %}"Add Project"{% endhl_text %}. Clicando sobre ele, a seguinte tela será mostrada. <br><br>

{% image fancybox left clear escolha_de_projeto.png 500px "Escolha o seu projeto." %}

<br>Escolha o seu projeto e clique em {% hl_text danger %}"Next"{% endhl_text %} você seguirá para a etapa de cadastro/login. Assim que o cadastro for concluído você já estará fornecendo seus recursos para o projeto.

{% image fancybox center boinc_seti.png "It's all over." %}

{% alert success fa-check-circle %}Parabéns por contribuir com a ciência!{% endalert %}


> Links Úteis:
> [Wikipedia do BOINC](https://pt.wikipedia.org/wiki/BOINC)
> [BOINC Projects](https://boinc.berkeley.edu/projects.php)

-----------------
<center> Sobre o autor: <br/> [www.brenohq.com](http://www.brenohq.com/) </center>
-----------------
