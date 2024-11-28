# project_m13
    _______________Módulo 13: Configurando o Django Rest Framework______________

    Aula 1: Introdução a Django Rest Framework

        ...

    Aula 2: Porque utilizar Restfull Api Frameworks e quais as opções disponíveis no mercado

        https://www.django-rest-framework.org/

        https://www.treinaweb.com.br/blog/o-que-e-o-django-rest-framework

        Django REST Framework ou DRF é uma biblioteca que permite a construção de APIs REST 
        utilizando a estrutura do Django. Lançado em Fevereiro de 2011, o DRF, por funcionar 
        sob a estrutura do Django, permite a construção de APIs em qualquer plataforma, seja 
        Windows, macOS ou Linux.

        É um framework muito utilizado por toda a comunidade, pois provê uma forma simples e rápida
        para a construção de APIs utilizando as facilidades que o Django oferece, como o sistema de 
        rotas e seu ORM para manipulação de banco de dados.


        - O que é ORM?

            https://www.devmedia.com.br/orm-object-relational-mapper/19056

            ORM (Object Relational Mapping) é uma técnica de mapeamento objeto-relacional que permite 
            a criação de uma ligação entre programas orientados a objetos e bancos de dados relacionais. 
            O ORM é um framework ou conjunto de classes que permite a interação entre o código e os sistemas 
            de bancos de dados, sem a necessidade de escrever códigos de conexão com o banco ou querys de SQL. 
            O ORM tem vários benefícios, como:

                - Abstração do banco de dados

                - Maior produtividade

                - Portabilidade

                - Segurança

                - Gerenciamento de relacionamentos

                - Facilidade de manutenção

                - Facilidade de trocar de banco de dados 

            O ORM segue padrões bem definidos, como o Data Mapper e o Active Record, que foram 
            definidos por Martin Fowler.


    Aula 3: Instalando Django Rest Framework

        - Temos outros framework de rest 

            - Tornado 

                https://www.tornadoweb.org/en/stable/

            - Fastapi

                https://fastapi.tiangolo.com/

            - Flask

                https://flask.palletsprojects.com/en/stable/


    Aula 3: Instalando Django Rest Framework

        https://www.django-rest-framework.org/#installation


    Aula 4: Configurando Django Rest Framework

        - Poetry

            Gerenciamento de dependências e empacotamento Python simplificado

            A poesia é uma ferramenta para gerenciamento e embalagem de dependência em Python. 
            Ele permite que você declare as bibliotecas das quais seu projeto depende e ele irá 
            gerenciá-las (instalar/atualizá-las) para você. Poesia oferece um lockfile para garantir 
            instalações repetíveis e pode construir seu projeto para distribuição.

            https://python-poetry.org/

            -Instalação

                - Instalação no ambiente global 

                    curl -sSL https://install.python-poetry.org | python3 -

                - Instalação no ambiente virtual

                    pip3 install poetry    

        -  Black            

            Formatador de código baseado no eslint

                https://black.readthedocs.io/en/stable/

                https://github.com/psf/black            

            - Instalando de forma global 

                sudo apt install black

    Aula 5: Gerenciando mudanças com o Django Migrations    

        - Crie um repositório e faça o clone 

        OBS!!!

            O professor instalou o Poetry no ambiente global porem na documentação e explicitamente 
            descrito que ele so deve ser instalado em um ambiente virtual para não haver conflitos 

             - Usando seu ambiente virtual
                Por padrão, o Poetry cria um ambiente virtual em {cache-dir}/virtualenvs. Você pode alterar 
                o cache-dirvalor editando a configuração do Poetry. Além disso, você pode usar a 
                virtualenvs.in-projectvariável de configuração para criar ambientes virtuais dentro do diretório do seu projeto.

                https://python-poetry.org/docs/basic-usage/#using-your-virtual-environment

        - Inicie o Poetry e instala as dependencia que você vai usar no projeto    

                poetry init 

                - Vamos instalar 

                    pytest
                    factory-boy

                - Ver as configurações informadas 

                        cat pyproject.toml

            -Quando criamos um venv iniciamos o projeto assim:

                - Inicindo um projeto com o poetry

                    poetry new <nome do projeto>                

        - Instalando o django com o poetry

            poetry add django     

        -  Iniciando um projeto com o poetry/django          

            poetry run django-admin.py startproject <nome do projeto> . 

                (O ponto indica para o django iniciar dentro do diretorio atual)

    Aula 5: Gerenciando mudanças com o Django Migrations

        - Iniciando o app com o django/poetry

            poetry run python3 manage.py startapp api

        - Rodando a migração    

            poetry run python3 manage.py migrate

        - Testando o setup do projeto 

            poetry run python3 manage.py runserver

    ____Módulo 14: Integrando Modelos e Serializers em Django Rest Framework____

    - Aula 1: Utlizando Django Serializers para tratar de modelos Django

        - O que é Serializers

            Os serializers DRF são componentes essenciais da estrutura. 
            Eles servem para traduzir entidades complexas, como querysets e
            instâncias de classe, em representações simples que podem ser usadas no
            tráfego da web, como JSON e XML, e chamamos esse processo de
            serialização. 
            Os serializers também servem para fazer o caminho oposto:
            desserialização. Isso é feito transformando representações simples (como
            JSON e XML) em representações complexas, instanciando objetos, por
            exemplo.

            - BaseSerializer: classe base para construir serializers genéricos. 

            - ModelSerializer: ajuda na criação de serializers baseados em modelos. 

            - HyperlinkedModelSerializer: Semelhante a ModelSerializer, porém retorna
            um link para representar o relacionamento entre entidades (ModelSerializer
            retorna, por padrão, o id da entidade relacionada).


    Aula 2: Como integrar Django Models e Django Serializers

        - Uma vantagem do Django e que podems isolar os nossos Apps

        - Crie um novo projeto

            EX: 
                poetry run python manage.py startapp order
                poetry run python3 manage.py startapp product

        - Vamos criar nossos modelos

            - Em /order crie:

                models/__init__.py

                    - Dentro de models crie:

                        order.py        

                - Detro de order delete:

                    models.py

            - Em /product crie:

                models/__init__.py

                    - Dentro de models crie:

                        product.py        

                - Detro de order delete:

                    models.py        


    Aula 3: Criando Django Models para serem usados em Django Serializers

        - O serializer atua entre as camadas de views e de models

            View set <------> serializer <------> models(banco de dados)

        - Ele traduz as informações entre essas camadas
        - Ele transforma informações complexas em formador como json e XML
        - Mas tambem pode fazer o caminho inverso 

        - Em product/models

            - Cole o codigo em product/models/product.py

                from django.db import models

                from product.models import Category


                class Product(models.Model):
                    title = models.CharField(max_length=100)
                    description = models.TextField(max_length=500, blank=True, null=True)
                    price = models.PositiveIntegerField(null=True)
                    active = models.BooleanField(default=True)
                    category = models.ManyToManyField(Category, blank=True)


            - Crie um arquivo chamado category.py e cole o codigo:

                from django.db import models

                from django.db import models

                class Category(models.Model):
                    title = models.CharField(max_length=100)
                    slug = models.SlugField(max_length=100, unique=True)
                    description = models.BooleanField(default=True)

                    def __unicode__(self):
                        return self.title

        - Em order/models

            - Em order.py Cole o código        

            from django.contrib.auth.models import User
            from django.db import models

            from product.models import Product

            class Order(models.Model):
                product = models.ManyToManyField(Product, blank=False)
                user = models.ForeignKey(User, on_delete=models.CASCADE)

        - Criando  a pasta serializers

            -Em order/ crie:

                serializers/__init__.py      

                - Em serializers/ crie:

                    order_serializers.py

            -Em product/ crie:

                serializers/__init__.py      

                - Em serializers/ crie:

                    product_serializer.py   
                    category_serializer.py       


    Aula 4: Migrando Django Models

        - Antes de termos nossos serializers e necessário termos nossos modelos

        - Agora precisamos gerar nossas migrações

        - Dentro das pastas dos apps tem um arquivo chamado admin.py
            - Importe seus modelos neste arquivo

                from .models import Product, Category

        - Dentro da pasta models no arquivo __init__.py importe seus modelos 

            from .product import Product
            from .category import Category     

        - Dentro das pastas dos apps tem um arquivo chamado admin.py
            - Importe seus modelos neste arquivo

                from .models import Order

        - Dentro da pasta models no arquivo __init__.py importe seus modelos 

            from .order import Order

        - Não se esqueça  de sempre excluir os diretórios com os memsos 
        nomes das pastas que estamos criando

            - Estamos seguindo um modelos de código limpo 
            - Sendo assim sempre criaremos pastas com nomes descritivos
            - E dentro destas pasta criaremos arquivos objetivos, fragmentando o código
            - Um código bem dividido e estruturado simplifica o processo de debug    
              
        - Vamos declarar nossos app dentro do bookstore/ settings.py

            - Adicione nosso apps dentro do INSTALLED_APPS

                INSTALLED_APPS = [
                    "django.contrib.admin",
                    "django.contrib.auth",
                    "django.contrib.contenttypes",
                    "django.contrib.sessions",
                    "django.contrib.messages",
                    "django.contrib.staticfiles",
                ->  "order",
                ->  "product",
                ]

    - Gerando as migrações

        - Criando migrações (cria nossos arquivos na pasta mitrations)

            poetry run python3 manage.py makemigrations

        - Eviando para o db

            poetry run python3 manage.py migrate    

    - Aula 5: Criando Serializers em Django

        - Vamos instalar o Django Rest Framework com o poetry

            poetry add django-rest-framework

        - Adicione os codigos no arquivos criados na pasta serializers/

        - Importe os serializers nos arquivos __init__.py


    - Aula 6: Criando Factories com Django Factory    

        - Vamos adicionar nossos Factories

            - Dentro dos applications crie um arquivo chamado:
                
                /order
                /product

                touch factories.py            