# Домашнее задание к занятию 9 «Процессы CI/CD»

## Подготовка к выполнению

1. Создайте два VM в Yandex Cloud с параметрами: 2CPU 4RAM Centos7 (остальное по минимальным требованиям).

   <img width="1222" alt="VM" src="https://github.com/user-attachments/assets/18c8d64c-7d25-4504-b0f5-c9588d3919ea">

2. Пропишите в [inventory](./infrastructure/inventory/cicd/hosts.yml) [playbook](./infrastructure/site.yml) созданные хосты.

   <img width="365" alt="Inventory" src="https://github.com/user-attachments/assets/e8a346d4-4ea6-42f9-8b92-75a8d052cf43">

3. Добавьте в [files](./infrastructure/files/) файл со своим публичным ключом (id_rsa.pub). Если ключ называется иначе — найдите таску в плейбуке, которая использует id_rsa.pub имя, и исправьте на своё.

   <img width="323" alt="Public_key" src="https://github.com/user-attachments/assets/e31ff02b-01a3-4445-9f45-be10b0c03b09">

   <img width="323" alt="Task_key" src="https://github.com/user-attachments/assets/1337caad-ae8e-49b1-8534-f0b6e13a84fa">

4. Запустите playbook, ожидайте успешного завершения.

   <img width="614" alt="Screen4" src="https://github.com/user-attachments/assets/f7063749-7e2b-47d6-86dd-03ac6cdfc6d8">

5. Проверьте готовность SonarQube через [браузер](http://localhost:9000).

   <img width="678" alt="Sonarqube" src="https://github.com/user-attachments/assets/d35ecc07-a1eb-4e72-b713-654fbf547a0f">

6. Зайдите под admin\admin, поменяйте пароль на свой.
7.  Проверьте готовность Nexus через [бразуер](http://localhost:8081).

   <img width="680" alt="Nexus" src="https://github.com/user-attachments/assets/e159b0c3-3f33-43fd-b8b2-5d2d4867109b">

8. Подключитесь под admin\admin123, поменяйте пароль, сохраните анонимный доступ.

## Знакомоство с SonarQube

### Основная часть

1. Создайте новый проект, название произвольное.

   <img width="676" alt="Sonar_project" src="https://github.com/user-attachments/assets/c5756891-4949-4e65-9754-15092109c240">

2. Скачайте пакет sonar-scanner, который вам предлагает скачать SonarQube.
3. Сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).

   <img width="487" alt="PATH" src="https://github.com/user-attachments/assets/c3d34078-efb9-455d-804c-d8a136fc0ec7">

4. Проверьте `sonar-scanner --version`.

   <img width="613" alt="Sonar-scanner version" src="https://github.com/user-attachments/assets/e8918f4c-55db-4046-9738-35c6fa65cd84">

5. Запустите анализатор против кода из директории [example](./example) с дополнительным ключом `-Dsonar.coverage.exclusions=fail.py`.

   <img width="687" alt="Start analyzer" src="https://github.com/user-attachments/assets/d32ac0d3-17cf-402c-8fa8-80a0ea4b1899">

6. Посмотрите результат в интерфейсе.

   <img width="685" alt="Result analyzer" src="https://github.com/user-attachments/assets/99048d48-8280-4dfd-b6b5-9145bab1f6b2">

   <img width="686" alt="Result analyzer Interface" src="https://github.com/user-attachments/assets/b2a2ae97-56b1-43b9-b143-9978e49826ac">

7. Исправьте ошибки, которые он выявил, включая warnings.
8. Запустите анализатор повторно — проверьте, что QG пройдены успешно.
9. Сделайте скриншот успешного прохождения анализа, приложите к решению ДЗ.

   <img width="682" alt="After_fix" src="https://github.com/user-attachments/assets/68c99597-e606-4d30-ba9f-7b5db8e0a291">


## Знакомство с Nexus

### Основная часть

1. В репозиторий `maven-public` загрузите артефакт с GAV-параметрами:

 *    groupId: netology;
 *    artifactId: java;
 *    version: 8_282;
 *    classifier: distrib;
 *    type: tar.gz.
   
2. В него же загрузите такой же артефакт, но с version: 8_102.
3. Проверьте, что все файлы загрузились успешно.

   <img width="484" alt="Maven downloads" src="https://github.com/user-attachments/assets/b4afffb5-d731-49e6-8b90-c79b0d28fe60">

4. В ответе пришлите файл `maven-metadata.xml` для этого артефекта.
   [maven-metadata](https://github.com/sash3939/CI-CD/blob/main/maven-metadata.xml)

### Знакомство с Maven

### Подготовка к выполнению

1. Скачайте дистрибутив с [maven](https://maven.apache.org/download.cgi).
2. Разархивируйте, сделайте так, чтобы binary был доступен через вызов в shell (или поменяйте переменную PATH, или любой другой, удобный вам способ).
3. Удалите из `apache-maven-<version>/conf/settings.xml` упоминание о правиле, отвергающем HTTP- соединение — раздел mirrors —> id: my-repository-http-unblocker.
4. Проверьте `mvn --version`.




5. Заберите директорию [mvn](./mvn) с pom.

### Основная часть

1. Поменяйте в `pom.xml` блок с зависимостями под ваш артефакт из первого пункта задания для Nexus (java с версией 8_282).
2. Запустите команду `mvn package` в директории с `pom.xml`, ожидайте успешного окончания.
3. Проверьте директорию `~/.m2/repository/`, найдите ваш артефакт.
4. В ответе пришлите исправленный файл `pom.xml`.

