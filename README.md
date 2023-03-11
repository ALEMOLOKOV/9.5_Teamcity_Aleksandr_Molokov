# 9.5_Teamcity_Aleksandr_Molokov

# Подготовка к выполнению
В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа jetbrains/teamcity-server.
Дождитесь запуска teamcity, выполните первоначальную настройку.
Создайте ещё один инстанс (2CPU4RAM) на основе образа jetbrains/teamcity-agent. Пропишите к нему переменную окружения SERVER_URL: "http://<teamcity_url>:8111".
Авторизуйте агент.
Сделайте fork репозитория.
Создайте VM (2CPU4RAM) и запустите playbook.

# Создание ВМ на YandexCloud

![virtual mashins](https://user-images.githubusercontent.com/109212419/224479017-0a169ba5-a4ca-4283-a158-8110eb8757cb.jpg)

# Запуск playbook для установки nexus

![Nexus развертывание playbook](https://user-images.githubusercontent.com/109212419/224479058-1ffa9d87-89b8-43e3-8566-c8bd8dd69765.jpg)

# Запуск Teamcity

![teamcity server first start](https://user-images.githubusercontent.com/109212419/224479083-305e8afa-44bf-4d11-a998-3103808a883f.jpg)


# Основная часть
Создайте новый проект в teamcity на основе fork.

![1 create config from fork](https://user-images.githubusercontent.com/109212419/224479917-2acfb4a3-0c4d-4716-8ead-399d2e70dc93.jpg)

Сделайте autodetect конфигурации.

![2 auto-detect config](https://user-images.githubusercontent.com/109212419/224480102-8a9b867a-a616-4e26-8491-839e593e6892.jpg)

Сохраните необходимые шаги, запустите первую сборку master.

![3 1 first build](https://user-images.githubusercontent.com/109212419/224481018-25c45601-486d-498c-a12b-0bd2db5e0e46.jpg)
![3 2 build logs](https://user-images.githubusercontent.com/109212419/224481028-3ab36c24-be16-40e5-857d-02aa00f7c340.jpg)

Поменяйте условия сборки: если сборка по ветке master, то должен происходит mvn clean deploy, иначе mvn clean test.

![4 change build config](https://user-images.githubusercontent.com/109212419/224481508-05352fc3-b36e-4698-8882-27efae4f5fa6.jpg)

Для deploy будет необходимо загрузить settings.xml в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.



В pom.xml необходимо поменять ссылки на репозиторий и nexus.


Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.


Мигрируйте build configuration в репозиторий.


Создайте отдельную ветку feature/add_reply в репозитории.


Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово hunter.


Дополните тест для нового метода на поиск слова hunter в новой реплике.


Сделайте push всех изменений в новую ветку репозитория.


Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.


Внесите изменения из произвольной ветки feature/add_reply в master через Merge.


Убедитесь, что нет собранного артефакта в сборке по ветке master.


Настройте конфигурацию так, чтобы она собирала .jar в артефакты сборки.


Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.


Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.


В ответе пришлите ссылку на репозиторий.
