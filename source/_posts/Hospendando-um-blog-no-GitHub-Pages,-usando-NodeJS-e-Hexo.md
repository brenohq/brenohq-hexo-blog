---
title: Hospendando um blog no GitHub Pages, usando NodeJS e Hexo
date: 2016-07-03 12:47:24
tags:
- NodeJS
- Blog
- Github

disqusIdentifier: fdsF34ff34
keywords:
- hospendando
- criando
- blog
- github
- pages
- usando
- nodeJS
- hexo
- grátis
- gratuitamente
- javascript
- html
- css
- brenohq
- Breno Henrique
- brenohq.com
- www.brenohq.com  
clearReading: false
thumbnailImage: https://avatars2.githubusercontent.com/u/6375567?v=3&s=400
thumbnailImagePosition: right
autoThumbnailImage: yes
metaAlignment: center
coverCaption: "É hora de codar!"
coverMeta: out
coverSize: partial
coverImage:
gallery:
comments: true
---

Hoje eu ensino como hospedar um blog gratuitamente no serviço [GitHub Pages](https://pages.github.com/). Vamos usar o [Hexo](https://hexo.io/), um módulo do NodeJS usado como framework para criação rápida e fácil de blogs. Posteriormente ensinarei como instalar e personalizar temas para essa plataforma. Então, pegue seu café e mãos na massa!

<!-- excerpt -->

-----------------

### Você vai precisar instalar algumas coisas antes de começar:
1. [NodeJS](http://nodejs.org/)
2. [Hexo](https://hexo.io/)

``` bash
$ npm install -g hexo
```

Você pode instalar globalmente com o argumento `-g`, mas se tiver alguma experiência pode colocar o pacote em seu package.json e depois dar um npm install no diretório do blog.

-----------------


### Criando a sua GitHub page
O GitHub disponibiliza um serviço de hospedagens para sites estáticos aqui: [GitHub Pages](https://pages.github.com/).

Crie um novo repositório com o nome nesse formato: **seuusername.github.io**

**Atenção:** O formato deve seguir esse padrão, caso contrário o github não considerará seu repositório como uma página válida.

Agora, com o repositório criado, é só clonar para a sua máquina.

``` bash
$ git clone /caminho/para/o/seu/repositório
```

-----------------

### Vamos configurar o Hexo
Dentro do diretório que você acabou de clonar para a sua máquina, dê os seguintes comandos:
``` bash
$ hexo init
$ npm install
```

Vamos abrir o arquivo de configuração `_config.yml`.
Altere o valor desses quatro atributos básicos:
{% code %}
title: O Blog do Breno
subtitle:
author: Breno Henrique
language: pt-BR
{% endcode %}

-----------------

### Configurando o deploy das postagens

Para fazer com que o deploys do GitHub funcionem, sua seção {% hl_text danger %}#Deployment{% endhl_text %} deve-se parecer com isso:

```md
deploy:
  type: git
  repo: git@github.com:brenohq/brenohq.github.io.git
  branch: master
```
Agora é só instalar o deployer:

``` bash
npm install hexo-deployer-git --save
```

-----------------

### Criando a primeira postagem

Para criar uma postagem é simples:
``` bash
hexo new "Post de Teste"
```

Pronto, você criou a primeira postagem. Agora vamos editá-la:
Dentro do diretório `/source` foi criado um arquivo `.md` com a sua postagem.

```md
---
title: Post Teste
date: 2016-07-03 13:58:33
tags:
---
```

Esse é seu post, você pode escrevê-lo como quiser, utilizando diversos recursos disponibilizados na [documentação completa do Hexo](https://hexo.io/docs/writing.html).

-----------------

### Realizando o primeiro deploy

Com a postagem editada, basta dar os seguintes comandos e seu blog vai estar atualizado.
``` bash
$ hexo generate
$ hexo deploy
```

{% alert success fa-check-circle %}Pronto, agora seu blog está atualizado e online!{% endalert %}

{% image fancybox right https://avatars2.githubusercontent.com/u/6375567?v=3&s=400 150px 150px %}



> Links Úteis:
> [GitHub Pages](https://pages.github.com/)
> [Documentação do Hexo](https://hexo.io/docs/)
> [Documentação do NodeJS](https://nodejs.org/en/docs/)

-----------------
<center> Sobre o autor: <br/> [www.brenohq.com](http://www.brenohq.com/) </center>
-----------------
