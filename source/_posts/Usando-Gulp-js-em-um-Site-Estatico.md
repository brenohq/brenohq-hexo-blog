---
title: Usando Gulp.js em um Site Estático de Forma Simples
date: 2017-01-21 17:31:12
tags:
- OpenSource
- Task Runners
- Tutorial
- JS

disqusIdentifier: fdsF34ff34
keywords:
- Task Runners
- Javascript
- Gulp
- Otimização
- CSS
- Desenvolvimento
- brenohq
- Breno Henrique
- brenohq.com
- www.brenohq.com  
clearReading: false
thumbnailImage: https://avatars0.githubusercontent.com/u/6200624?v=3&s=400
thumbnailImagePosition: right
autoThumbnailImage: yes
metaAlignment: center
coverCaption: "Hoje vamos aprender a adicionar o Gulp em nossos projetos!"
coverMeta: out
coverSize: partial
coverImage: https://scotch.io/wp-content/uploads/2014/11/automate-tasks-gulpjs.png
gallery:
comments: true

---

O [Gulp](gulpjs.com), como o próprio site diz, é um kit de ferramentas para automatizar tarefas dolorosas e demoradas em nosso workflow. Nesse tutorial, vamos pegar um site e automatizar todo o seu processo de build, desde tarefas como a otimização das imagens, até o bundle de nosso javascript/css. Sigam-me os bons! 

<!-- more -->

-----------------

## Requisitos
Para esse tutorial, vou assumir que vocês já estejam com o [Node](https://nodejs.org/en/) e o [NPM](https://www.npmjs.com) instalado e funcionando em vossas máquinas.

``` bash
$ node --version
$ npm --version
```

## Instalando o Gulp em nossa máquina

Para instalar o Gulp globalmente em nossa máquina, basta o seguinte comando:

``` bash
$ sudo npm i -g gulp
```

Com isso, teremos o gulp a nosso dispor. Agora é hora de configurá-lo. Vou utilizar o diretório "MeuSite" como exemplo. Mas a aplicação real desse arquivo de configuração que criaremos, está sendo feita nesse meu [repositório no GitHub](https://github.com/brenohq/site4LEC), onde desenvolvi um pequeno site para um evento sobre sofware livre que irá acontecer em minha universidade. Let's do it!

``` bash
$ cd MeuSite
$ touch gulpfile.js
```

## Escrevendo sua primeira task

Agora, sem lero lero, vamos abrir o arquivo e começar a codar. Vamos adicionar o seguinte trecho em nosso arquivo.

~~~ javascript
  const  gulp = require('gulp'),
         concat = require('gulp-concat');

  gulp.task('pack-js', function() {
    return gulp.src(['caminho_para_arquivo1.js', 'diretorio/*.js', 'diretorio/**/*.js']) // Escolha os arquivos/diretórios
      .pipe(concat('bundle.js')) // O gulp-concat sendo usado 
      .pipe(gulp.dest('public/js')); // Resultado em public/js/bundle.js
  });
~~~


Esse código é responsável por concatenar todos os arquivos que forem passados no array como primeiro argumento em gulp.src(), o resultado poderá ser observado em public/js/bundle.js. Você pode passar tanto arquivos específicos, como diretórios inteiros.

Agora vamos instalar o gulp-concat, também vamos colocá-lo nas dependências de desenvolvimento.

``` bash
$ npm i --save-dev gulp-concat
```

Depois basta executar nossa tarefa com o comando a seguir:

``` bash
$ gulp pack-js
```

Demais não é?

-----------------

## Escrevendo outras tarefas

Agora vou acelerar um pouco mais. Vamos adicionar todo o código a seguir, mas não se preocupe, vou explicá-lo por partes logo em seguida. Vamos lá!

~~~ javascript
// Importando todos os plugins que utilizei nesse site
const
  gulp = require('gulp'),
  concat = require('gulp-concat'),
  imagemin = require('gulp-imagemin'),
  rename = require('gulp-rename'),
  uncss = require('gulp-uncss'),
  htmlmin = require('gulp-htmlmin'),
  size = require('gulp-size'),
  sizereport = require('gulp-sizereport'),
  runSequence = require('run-sequence');

gulp.task('pack-js', function() {
  // Fazendo o bundle de todos arquivos javascript
  return gulp.src(['node_modules/jquery/dist/jquery.min.js', 'node_modules/jquery-scrollify/jquery.scrollify.min.js', 'src/js/scroll.js', 'src/js/nav.js'])
    .pipe(concat('bundle.js'))
    .pipe(gulp.dest('public/js'));
});

gulp.task('pack-css', function() {
  // Concatenando também todos os arquivos CSS
  return gulp.src(['src/css/reset.css', 'src/css/bulma.css', 'src/css/style.css'])
    .pipe(concat('stylesheet.css'))
    .pipe(gulp.dest('public/css'));
});

gulp.task('imagemin', () =>
  // Otimizando as imagens do site
  gulp.src('src/img/**/*')
  .pipe(imagemin())
  .pipe(gulp.dest('public/img'))
);

gulp.task('minify-html', function() {
  // Minificando o index.html
  return gulp.src('src/index.html')
    .pipe(htmlmin({
      collapseWhitespace: true
    }))
    .pipe(gulp.dest('public/'));
});

gulp.task('remove-unused-css', function() {
  // Removendo do nosso CSS todos as definições que não são necessárias em nosso projeto
  return gulp.src('public/css/stylesheet.css')
    .pipe(uncss({
      html: ['src/index.html']
    }))
    .pipe(gulp.dest('./public/css/stylesheet.min.css'));
});

gulp.task('sizereport', function() {
  // Exibe uma mensagem contendo informações sobre o tamanho de nossos arquivos pós otimizações
  return gulp.src('./public/**/*')
    .pipe(sizereport());
});

gulp.task('default', function(done) {
  // Task que será executada quando dermos o comando "gulp"
  runSequence('pack-js', 'pack-css', 'imagemin', 'minify-html', 'remove-unused-css', 'sizereport', function() {
    done();
  });
});
~~~

Nas primeiras linhas desse código, definimos os plugins que estamos utilizando. Você pode encontrá-los facilmente fazendo uma busca no [Npm](https://www.npmjs.com/search?q=gulp-imagemin). Acredito que você tenha percebido como funciona a separação de tarefas no gulp, e como será fácil usar os plugins que você desejar.

~~~ javascript
  gulp.task('nome-da-tarefa', function() {
  // Chamadas dos plugin, mensagens a serem exibidas, e escrita dos arquivos otimizados
  });
~~~

-----------------

Por último, é importante explicar a forma que podemos executar nossas tarefas de forma síncrona, com o plugin [run-sequence](https://www.npmjs.com/package/run-sequence). 

~~~ javascript
gulp.task('default', function(done) {
  // Task que será executada quando dermos o comando "gulp"
  runSequence('pack-js', 'pack-css', 'imagemin', 'minify-html', 'remove-unused-css', 'sizereport', function() {
    done();
  });
});
~~~

Como definimos o nome dessa task como "default", ela poderá ser executada com o comando {% hl_text danger %}gulp{% endhl_text %} diretamente. Nesse exemplo que utilizei, o build do site é feito para o diretório /public, fique livre para modificar o código para o seu projeto.

{% alert success fa-check-circle %}That's all folks! Obrigado!{% endalert %}


> Links Úteis:
> [Framework Usado Nesse Exemplo](bulma.io)
> [2017 is the year that front-end developers should go back and master the basics](https://medium.freecodecamp.com/what-to-learn-in-2017-if-youre-a-frontend-developer-b6cfef46effd#.f9xd9e32r)
> [Hospendando um blog no GitHub Pages, usando NodeJS e Hexo](https://brenohq.github.io/2016/07/03/Hospendando-um-blog-no-GitHub-Pages,-usando-NodeJS-e-Hexo/)

-----------------
<center> Sobre o autor: <br/> [www.brenohq.com](http://www.brenohq.com/) </center>
-----------------
