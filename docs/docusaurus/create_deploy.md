---
title: 'Развертывание сайта'
---

Развертывание сайта в интернете на платформе GitHub требует создания отдельного репозитория, 
в котором будет храниться интернет контент. **Поясним.** Исходники сайта - это всего лишь набор требуемых для генератора Docusaurus файлов, 
которые сами по себе интернет контентом не являются. Интернет контент появляется при выполнении определенных команд в консоли каталога локального сайта.

При создании репозитория могут быть два варианта:
1. Предполагается, что сайт будет только один и расположен по базовому адресу
2. Базовый сайт уже существует, но требуется еще один сайт (новый сайт)

Важным для любого из вариантов является наличие репозитория с предопределенным именем: имя_аккаунта.github.io. 
Это имя фактически является частью интернет адреса, по которому будет расположен сайт или сайты.   
Для нашего примера MyGit.github.io. 

Эту схему можно представить, как список адресов сайтов:  
- https: // mygit.github.io / - базовый сайт
- https: // mygit.github.io / site 1 / - новый сайт 1
- https: // mygit.github.io / site N / - новый сайт N

Таким образом сайтов можно создать много. Каждый созданный сайт - это свой репозиторий и доступ к нему может быть отрегулирован, как Public или Private. 


## Создание репозитория для развертывания сайта

1.  Создаем репозиторий  
    ![](img/create_deploy1.png)  
    1\. Имя репозитория (Repository name):

        - базовый сайт - mygit.github.io  
        - новый сайт - например, smydocs   

    2\. Описание репозитория, например: Интернет контент ...       
    3\. Выбираем, какой будет репозиторий:  

    - Puplic - доступный всем для просмотра.   
    - Private - доступный тем, кто имеет разрешения.     

    4\. Обязательно ставим галку "Add a README file" для инициализации репозитория  
      
2.  После создания репозитория надо указать, что репозиторий имеет отношение к GitHub Pages и должен размещать интернет контент. 
Для этого выбираем пункт Settings в горизонтальном меню  
    ![](img/create_deploy2.png)  
    На открывшейся странице  
    ![](img/create_deploy3.png)  
    1\. Выбираем пункт Pages  
    2\. Выбираем main  
    3\. Нажимаем кнопку Save (сохранить)  


## Настройка конфигурационного файла

Создав репозиторий на стороне GitHub мы обеспечили размещение интернет контента, 
но сам установленный на ПК Docusaurus ни чего не "знает" ни о каких репозиториях. 
Поэтому, необходимо провести настройку конфигурационного файла docusaurus.config.js, который лежит в корне проекта изменением некоторых свойств.

| Свойства          | Базовый сайт              | Новый сайт                | Примечание                                           |
|-------------------|---------------------------|---------------------------|------------------------------------------------------|
| title             | 'Базовый сайт'            | 'Новый сайт'              | любое значение                                       |
| tagline           | 'base'                    | 'mydocs'                  | любое значение                                       |
| baseUrl           | '/'                       | '/smydocs/'               | всегда<br/>для нового сайта <br/>это имя репозитория |
| url               | 'https://mygit.github.io' | 'https://mygit.github.io' | базовый URL                                          |
| organizationName  | 'mygit'                   | 'mygit'                   | имя аккаунта                                         |
| projectName       | 'mygit.github.io'         | 'smydocs'                 | имя репозитория                                      |
| deploymentBranch  | 'main'                    | 'main'                    | всегда                                               |


## Развертывание сайта

Для развертывания сайта на платформе GitHub необходимо выполнить ряд команд в консоли проекта:

- **yarn build** - создание интернет контента из исходников. При выполнении команды будет создан каталог build, который будет содержать интернет контент.
- **yarn serve** - проверка, что создаваемый сайт однозначно запуститься в интернет. Выполнять все время не надо, только если возникли ошибки.
- **yarn deploy** - передача созданного интернет контента в отдельный репозиторий на GitHub отмеченный как Pages, для запуска механизмов развертывания сайта.