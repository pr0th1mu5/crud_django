# Etapa final - crud_django
Tutorial para aprendizado de construção de um CRUD em django


  > Esse tutorial segue a sequência de código do site oficial da documentação Django disponível [Aqui!](https://docs.djangoproject.com/en/5.0/intro/tutorial01/)

> [!important]
> Para fazer essa atividade é importante lembrar que:
> 
> `cd`     acessa um diretório no terminal linux;
> 
> `cd` ..  volta um diretório no terminal linux;
> 
> `touch`  cria um novo documento no terminal linux;
> 
> `vim`    é um editor de texto no terminal que você pode utilizar, ou use o vsCode se preferir.
>
> `ls -l`  lista todos os arquivos de um diretório no terminal linux.

<hr />

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
Com esse comando, tabelas que precisam ser criadas serão criadas se necessárias.

10 - Acesse o diretório `polls` e edite o arquivo `models.py`inserindo o código abaixo:

```python
from django.db import models

class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField("date published")


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)n

```

11 - Agora vá até o diretório do projeto `mysite` e edite o arquivo `settings.py`para inserirmos sua aplicação no campoi INSTALLED_APPS conforme abaixo:

```python
INSTALLED_APPS = [
    "polls.apps.PollsConfig",
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

Nesse momento, o Django incluiu sua aplicação criada à sua estrutura. 

12 - No diretório do projeto `mysite`, execute a linha a seguir:

```python
$ python manage.py makemigrations polls

```

Irá aparecer algo similar a:

```python
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
```

13 - O comando abaixo irá executar migrações no banco de dados e gerar o código SQL do nosso banco em tempo de execução (sqLite).

```python
$ python manage.py sqlmigrate polls 0001

```

14 - Execute novamente o comando migrate:
```python
$ python manage.py migrate

```

15 - Na pasta da aplicação `polls`, edite novamente o arquivo models.py de forma que fique com o código a seguir:

```python
from django.db import models
import datetime
from django.utils import timezone

class Question(models.Model):
    # ...
    def __str__(self):
        return self.question_text
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)


class Choice(models.Model):
    # ...
    def __str__(self):
        return self.choice_text
```

15 - Criando um usuário admin. Retorne à pasta do seu projeto `mysite`, e execute o comando python abaixo. é importante que você lembre das credenciais que irá criar.

```python
$ python manage.py createsuperuser

```


16 - Inicie o servidor novamente com `python manage.py runserver`. Acesse no browser o endereço http://localhost:8000/admin/
    
    
    > Perceba que um painel de administração do django lhe será apresentado. Insira suas credenciais criadas lá.



