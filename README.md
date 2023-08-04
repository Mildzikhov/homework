### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).   
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

![Image alt](https://github.com/mildzikhov01/gitlab/blob/main/img/1.png)

---

### Задание 2

**Что нужно сделать:**

1. Запушьте [репозиторий](https://github.com/netology-code/sdvps-materials/tree/main/gitlab) на GitLab, изменив origin. Это изучалось на занятии по Git.
2. Создайте .gitlab-ci.yml, описав в нём все необходимые, на ваш взгляд, этапы.

В качестве ответа в шаблон с решением добавьте: 
   
 * файл gitlab-ci.yml для своего проекта или вставьте код в соответствующее поле в шаблоне; 
 * скриншоты с успешно собранными сборками.
 
 ```
 stages:
  - test
  - build

test:
  stage: test
  image: golang:1.17
  script:
   - go test .

static-analysis:
 stage: test
 image:
  name: sonarsource/sonar-scanner-cli
  entrypoint: [""]
 variables:
 script:
  - sonar-scanner -Dsonar.projectKey=my-project1 -Dsonar.sources=. -Dsonar.host.url=http://130.193.36.200:9000/ -Dsonar.login=sqp_c54e4da7581c1413b62ed3cb5ea40455f23ce376

build_manual:
 stage: build
 except:
 - master
 image: docker:latest
 script:
 - docker build .

build:
  stage: build
  image: docker:latest
  script:
   - docker build .

 ```
 
![Image alt](https://github.com/mildzikhov01/gitlab/blob/main/img/2.png)
 
