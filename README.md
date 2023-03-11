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

![5 manage setting](https://user-images.githubusercontent.com/109212419/224482033-7344975c-00c6-4197-ad6f-adc5a78a331c.jpg)

В pom.xml необходимо поменять ссылки на репозиторий и nexus.

![6 change pom_xml](https://user-images.githubusercontent.com/109212419/224507458-4adf5a9b-0826-4982-b1c5-6338a9156219.jpg)

Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

![7 nexus](https://user-images.githubusercontent.com/109212419/224508102-f40e7d40-4fae-4d8b-b45b-6a5f335e4f53.jpg)

Мигрируйте build configuration в репозиторий.

![8 migration to git rep](https://user-images.githubusercontent.com/109212419/224508589-2976633b-4ac8-499f-932c-1a66a69d0f58.jpg)

![Ссылка на .teamcity](https://github.com/ALEMOLOKOV/example-teamcity/tree/master/.teamcity)

Создайте отдельную ветку feature/add_reply в репозитории.

![9 new branch](https://user-images.githubusercontent.com/109212419/224508882-7052f3ee-467b-43d4-a496-c8c8e46184d0.jpg)

Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово hunter.

![10 change welcomer](https://user-images.githubusercontent.com/109212419/224509388-5bd45e26-d146-4338-b11f-fee4a10ef5ec.jpg)

Дополните тест для нового метода на поиск слова hunter в новой реплике.

![11 chenge welcomertest](https://user-images.githubusercontent.com/109212419/224510131-89c5ba33-7539-454a-a6a6-21302391a50b.jpg)

Сделайте push всех изменений в новую ветку репозитория.

Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.

![13 build on new branch is ok](https://user-images.githubusercontent.com/109212419/224510307-0d2ff2aa-b302-46d7-b224-0252eb54c8ca.jpg)

Внесите изменения из произвольной ветки feature/add_reply в master через Merge.

![merge](https://github.com/aragastmatb/example-teamcity/commit/e9f263006035da1ac5c1ae32bb6c67010c83e1ea)

Убедитесь, что нет собранного артефакта в сборке по ветке master.

Настройте конфигурацию так, чтобы она собирала .jar в артефакты сборки.

![16 change build](https://user-images.githubusercontent.com/109212419/224511615-4534ad9b-0f8c-4b17-bfea-0ce66a355b9a.jpg)

Проведите повторную сборку мастера, убедитесь, что сбора прошла успешно и артефакты собраны.

![17 artefacts](https://user-images.githubusercontent.com/109212419/224511729-d17080b4-64cb-4ee2-9023-bfdb5d0f4e2c.jpg)

Проверьте, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.

![18 checking change in repo](https://user-images.githubusercontent.com/109212419/224511807-360743f9-3ad0-4a05-9b45-6ef37e48270a.jpg)


В ответе пришлите ссылку на репозиторий.

![Ссылка на репозиторий](https://github.com/ALEMOLOKOV/example-teamcity.git)
