# crud_django
Tutorial para aprendizado de construção de um CRUD em django


  > Esse tutorial segue a sequência de código do site oficial



1 - Prepare seu ambiente de desenvolvimento;

2 - Ative o seu ambiente de desenvolvimento antes de iniciarmos um projeto django;

3 - Crie um projeto django com comando abaixo:

```python
$ django-admin startproject mysite
```

4 - Acesse a pasta do seu projeto `mysite` criada e digite o comando abaixo:

```python
$ python manage.py runserver
```
Nesse momento seu servidor web será executado e estará acessível pelo navegador no endereço: `https://localhost:8000`

Para parar o servidor, no terminal use as teclas de atalho CTRL+C.

5 - Dentro do diretório do seu projeto, observe que se consegue ver o arquivo `manage.py`. Caso consiga, esse é o diretório principal. Execute o comando abaixo:

```python
$ python manage.py startapp polls
```

6 - Acesse o diretório da aplicação criada, `polls`, e edite o arquivo `views.py`. Insira o código abaixo:

```python
from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")
```

7 - No diretório polls, crie um arquivo chamado `urls.py` e insira o código a seguir:

```python
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index"),
]
```

8 - Retorne para a pasta do projeto (mysite) e execute o comando para rodar o servidor do passo 4. E acesse agora `localhost:8000/polls/

9 - Agora, ainda no diretório do projeto (mysite), execute o comando abaixo:

```python
$ python manage.py migrate
```


